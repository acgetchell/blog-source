Title: Enterprise Library authentication
Date: 2007-09-22 23:40
Author: Adam Getchell (noreply@blogger.com)
Tags: .net
Slug: enterprise-library-authentication

[Doug Rohrer](http://weblogs.asp.net/drohrer/), one of
[Avanade](http://www.avanade.com/) guys who worked on the Enterprise
Library, has posted a fantastic End to End Enterprise Library project
which incorporates the EL into ASP.NET and Winforms applications.  
  
Using Collin Collier's wonderful [Copy Source As
HTML](http://www.jtleigh.com/people/colin/software/CopySourceAsHtml/)
makes blogging the code much easier.  
  
Looking at Doug's work, we run into the common pattern of writing a base
page class which all asp.net pages inherit. Then he overrides the OnInit
function to kickstart authentication.  
  
I've been using an [ASP.NET Http
Module](http://support.microsoft.com/default.aspx?scid=kb;%5BLN%5D;Q307996)
to trap OnAuthenticate, but this is an interesting approach. Here's
Dougs BasePage class:  
  

<div class="cf">

<span class="cb1">using</span> System;

<span class="cb1">using</span>
Microsoft.Practices.EnterpriseLibrary.Security;

<span class="cb1">using</span> SecCache =
Microsoft.Practices.EnterpriseLibrary.Security.Cache;

<span class="cb1">using</span>
Microsoft.Practices.EnterpriseLibrary.Configuration;

<span class="cb1">using</span> System.Web.Security;

<span class="cb1">using</span> System.Security.Principal;

<span class="cb1">using</span> EntLibCommonCSharp;

 

 

<span class="cb1">namespace</span> EntLibWebCSharp

{

    <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\<summary\></span>

    <span class="cb2">///</span><span class="cb3"> Summary description
for BasePage.</span>

    <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\</summary\></span>

    <span class="cb1">public</span> <span class="cb1">class</span>
BasePage: System.Web.UI.Page

    {

 

<span class="cb1">        \#region</span> Private Variables

 

        <span class="cb1">private</span> IAuthenticationProvider
\_authenProvider;

        <span class="cb1">private</span> IAuthorizationProvider
\_authorProvider;

        <span class="cb1">private</span> IRolesProvider \_rolesProvider;

        <span class="cb1">private</span> ISecurityCacheProvider
\_secCacheProvider;

        <span class="cb1">private</span> IPrincipal \_principal;

        <span class="cb1">private</span>
EntLibCommonCSharp.AppConfigData \_config;

 

<span class="cb1">        \#endregion</span>

 

<span class="cb1">        \#region</span> Public Properties

 

        <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\<summary\></span>

        <span class="cb2">///</span><span class="cb3"> An Enterprize
Library Authentication Provider instance. </span>

        <span class="cb2">///</span><span class="cb3"> Used to determine
if a user's credentials are valid.</span>

        <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\</summary\></span>

        <span class="cb1">internal</span> IAuthenticationProvider
AuthenProvider {

            <span class="cb1">get</span> {

                <span class="cb1">if</span> (<span
class="cb1">null</span>==\_authenProvider) {

                    \_authenProvider =
AuthenticationFactory.GetAuthenticationProvider();

                }

                <span class="cb1">return</span> \_authenProvider;

            }

        }

 

        <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\<summary\></span>

        <span class="cb2">///</span><span class="cb3"> An Enterprize
Library Authorization Provider instance. </span>

        <span class="cb2">///</span><span class="cb3"> Used to determine
if a user is permitted to perform a certain action.</span>

        <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\</summary\></span>

        <span class="cb1">internal</span> IAuthorizationProvider
AuthorProvider {

            <span class="cb1">get</span> {

                <span class="cb1">if</span> (<span
class="cb1">null</span>==\_authorProvider) {

                    \_authorProvider =
AuthorizationFactory.GetAuthorizationProvider();

                }

                <span class="cb1">return</span> \_authorProvider;

            }

        }

 

        <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\<summary\></span>

        <span class="cb2">///</span><span class="cb3"> An Enterprize
Library Roles Provider instance. </span>

        <span class="cb2">///</span><span class="cb3"> Used to retrieve
a principal object given an identity.</span>

        <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\</summary\></span>

        <span class="cb1">internal</span> IRolesProvider RolesProvider {

            <span class="cb1">get</span> {

                <span class="cb1">if</span> (<span
class="cb1">null</span>==\_rolesProvider) {

                    \_rolesProvider = RolesFactory.GetRolesProvider();

                }

                <span class="cb1">return</span> \_rolesProvider;

            }

        }

 

        <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\<summary\></span>

        <span class="cb2">///</span><span class="cb3"> An Enterprize
Library Security Cache Provider instance.</span>

        <span class="cb2">///</span><span class="cb3"> Used to store and
retrieve a principal object given a security token.</span>

        <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\</summary\></span>

        <span class="cb1">internal</span> ISecurityCacheProvider
SecCacheProvider {

            <span class="cb1">get</span> {

                <span class="cb1">if</span> (<span
class="cb1">null</span>==\_secCacheProvider) {

                    \_secCacheProvider =
SecurityCacheFactory.GetSecurityCacheProvider();

                }

                <span class="cb1">return</span> \_secCacheProvider;

            }

        }

 

        <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\<summary\></span>

        <span class="cb2">///</span><span class="cb3"> The current
principal</span>

        <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\</summary\></span>

        <span class="cb1">internal</span> IPrincipal Principal {

            <span class="cb1">get</span> {

                <span class="cb1">return</span> \_principal;

            }

        }

 

        <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\<summary\></span>

        <span class="cb2">///</span><span class="cb3"> Provides easy
access to configuration data in the application config file.</span>

        <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\</summary\></span>

        <span class="cb1">internal</span> AppConfigData Config {

            <span class="cb1">get</span> {

                <span class="cb1">if</span> (<span
class="cb1">null</span>==\_config) {

                    \_config =
(AppConfigData)ConfigurationManager.GetConfiguration(AppConfigManager.SectionName);

                }

                <span class="cb1">return</span> \_config;

            }

        }

 

        <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\<summary\></span>

        <span class="cb2">///</span><span class="cb3"> Sets the
principal for this page request.</span>

        <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\</summary\></span>

        <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\<param name="principal"\></span><span class="cb3">The
principal to use for the rest of the request.</span><span
class="cb2">\</param\></span>

        <span class="cb1">internal</span> <span class="cb1">void</span>
SetPrincipal(IPrincipal principal) {

            \_principal = principal;

        }

 

 

<span class="cb1">        \#endregion</span>

 

        <span class="cb1">public</span> BasePage()

        {

            <span class="cb3">// No constructor necessary</span>

        }

 

 

        <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\<summary\></span>

        <span class="cb2">///</span><span class="cb3"> Fires at the
beginning of the page lifecycle.  Overriden here to retrieve principal
data from the</span>

        <span class="cb2">///</span><span class="cb3"> Enterprise
Library Security Cache provider or, if unable, to redirect to he login
page.</span>

        <span class="cb2">///</span><span class="cb3"> The Login.aspx
page will add the appropriate token via the ASP.NET forms authentication
cookie</span>

        <span class="cb2">///</span><span class="cb3"> if the user
successfully logs in.</span>

        <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\</summary\></span>

        <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\<param name="e"\>\</param\></span>

        <span class="cb1">protected</span> <span
class="cb1">override</span> <span class="cb1">void</span>
OnInit(EventArgs e) {

            <span class="cb1">base</span>.OnInit(e);

            <span class="cb3">// Make sure to skip this step if you're
already on the login page</span>

            <span class="cb1">if</span>
(ResolveUrl("\~/Login.aspx")!=Request.Url.AbsolutePath) {

                <span class="cb1">try</span> {

                    <span class="cb3">// Load the principal from the
FormsAuthentication ticket information.</span>

                    FormsAuthenticationTicket ticket =
FormsAuthentication.Decrypt((<span
class="cb1">string</span>)Request.Cookies[FormsAuthentication.FormsCookieName].Value);

                    GuidToken token = <span class="cb1">new</span>
GuidToken(<span class="cb1">new</span> System.Guid(ticket.UserData));

                    IPrincipal principal =
SecCacheProvider.GetPrincipal(token);

                    <span class="cb1">if</span> (<span
class="cb1">null</span>==principal) {

                        Response.Redirect("\~/Login.aspx");

                    } <span class="cb1">else</span> {

                        SetPrincipal(principal);

                    }

                } <span class="cb1">catch</span> (Exception) {

                    <span class="cb3">// If we have any issues, redirect
to Login</span>

                    Response.Redirect(ResolveUrl("\~/Login.aspx"));

                }

            }

        }

 

 

    }

}

</div>

  
  
Cool stuff!

</p>

