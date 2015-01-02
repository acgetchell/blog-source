Title: Using Enterprise Library Logging
Date: 2007-09-22 23:40
Author: Adam Getchell (noreply@blogger.com)
Tags: .net
Slug: using-enterprise-library-logging

To get logging working without pesky WMI/Performance counter errors on
<span style="font-style: italic;">every</span> logged event:  
  
Per [Tom Hollander's
weblog](http://weblogs.asp.net/tomholl/archive/2005/02/18/376187.aspx#FeedBack)  
  
Go to the Logging project, Project Properties dialog for the Common
project, and under Configuration Properties\\Build, find the Conditional
Compilation Properties property and remove ;USEWMI;USEPERFORMANCECOUNTER
for the build type you're interested in (ReleaseFinal, in this case).  
  
Ignore compile warnings about DB2 goop.  
  
Delete any old project references and re-add reference to new version in
C:\\Program Files\\Microsoft Enterprise
Library\\src\\Logging\\bin\\ReleaseFinal.  
  
Then add an appropriate using statement and use in code:  
  

<div class="cf">

<span class="cb1">using</span> System;

<span class="cb1">using</span> System.Collections;

<span class="cb1">using</span> System.ComponentModel;

<span class="cb1">using</span> System.Data;

<span class="cb1">using</span> System.Drawing;

<span class="cb1">using</span> System.Web;

<span class="cb1">using</span> System.Web.SessionState;

<span class="cb1">using</span> System.Web.UI;

<span class="cb1">using</span> System.Web.UI.WebControls;

<span class="cb1">using</span> System.Web.UI.HtmlControls;

<span class="cb1">using</span>
Microsoft.Practices.EnterpriseLibrary.Logging;

<span class="cb1">using</span>
Microsoft.Practices.EnterpriseLibrary.Logging.Tracing;

 

<span class="cb1">namespace</span> CAESDO

{

    <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\<summary\></span>

    <span class="cb2">///</span><span class="cb3"> Summary description
for WebForm1.</span>

    <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\</summary\></span>

    <span class="cb1">public</span> <span class="cb1">class</span>
DefaultPage : System.Web.UI.Page

    {

        <span class="cb1">private</span> <span class="cb1">void</span>
Page\_Load(<span class="cb1">object</span> sender, System.EventArgs e)

        {

            <span class="cb3">// Put user code to initialize the page
here</span>

            LogEntry logEntry = <span class="cb1">new</span> LogEntry();

            logEntry.Message = "Starting up the application";

            Logger.Write(logEntry);

 

            <span class="cb3">// Now this is cool! Tracing flow of code
through application</span>

            <span class="cb3">// and it was simple to add an EmailAlert
with an EmailSink</span>

 

            <span class="cb1">using</span> (<span class="cb1">new</span>
Tracer("Trace"))

            {

                Logger.Write("Hello world");

                Logger.Write("Hello by e-mail",
"EmailAlerts",5,3000,Microsoft.Practices.EnterpriseLibrary.Logging.Severity.Information,
"An e-mail message logging all kinds of stuff");

            }

 

        }

 

<span class="cb1">        \#region</span> Web Form Designer generated
code

        <span class="cb1">override</span> <span
class="cb1">protected</span> <span class="cb1">void</span>
OnInit(EventArgs e)

        {

            <span class="cb3">//</span>

            <span class="cb3">// CODEGEN: This call is required by the
ASP.NET Web Form Designer.</span>

            <span class="cb3">//</span>

            InitializeComponent();

            <span class="cb1">base</span>.OnInit(e);

        }

 

        <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\<summary\></span>

        <span class="cb2">///</span><span class="cb3"> Required method
for Designer support - do not modify</span>

        <span class="cb2">///</span><span class="cb3"> the contents of
this method with the code editor.</span>

        <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\</summary\></span>

        <span class="cb1">private</span> <span class="cb1">void</span>
InitializeComponent()

        {   

            <span class="cb1">this</span>.Load += <span
class="cb1">new</span> System.EventHandler(<span
class="cb1">this</span>.Page\_Load);

        }

<span class="cb1">        \#endregion</span>

    }

}

</div>

  
  
<span style="font-style: italic;">Voila!</span>  
  
It'd sure make it easier to post code to my weblog if VisualStudio 2005
included
[CopySourceAsHtml](http://www.jtleigh.com/people/colin/software/CopySourceAsHtml/)
functionality. This is a great application, too bad it doesn't work for
me. I seem to have uncovered the first interaction between CSAH and a
trial VisualPerl installation that won't uninstall.  
  
Par for the course.  
  
Although, I've suggested to the Visual Studio 2005 guys that they add
this feature.  
  
P.S. Collin worked to fix CSAH, and I nuked and reinstalled my system,
including Visual Studio 2003.NET. That seems to have done the trick.

</p>

