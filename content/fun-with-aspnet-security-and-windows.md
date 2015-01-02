Title: Fun with ASP.NET security and Windows 2003 SP1 breakage
Date: 2007-09-22 23:40
Author: Adam Getchell
Tags: .net
Slug: fun-with-aspnet-security-and-windows
Category: Programming

Problem: you want secure database access, using a connection string like
this:

<div class="cf">

<span class="cb1">\<</span><span class="cb2">add</span><span
class="cb3"></span><span class="cb4">key</span><span
class="cb1">="DatabaseConnection"</span><span class="cb3"></span><span
class="cb4">value</span><span class="cb1">="server=SERVER;Persist
Security Info=False;database=DATABASE;Integrated
Security=SSPI;"/\></span>

</div>

Solution: First, we're running IIS6.0. So we can set up a separate
Application Pool, and setup credentials for that application pool to
use.

We <span style="FONT-WEIGHT: bold;">don't</span> want to use
Impersonation, because then our connection credentials will run as the
application user, which may be different for each request, which will
slow database access down because we won't be able to use database
connection pooling.

We <span style="FONT-WEIGHT: bold;">don't</span> want to use a domain
account, because exploiting that account gives a free ride (and
reconnaissance) to our entire network.

We <span style="FONT-WEIGHT: bold;">do</span> want to use a local
account, with minimal rights on the Windows 2003/IIS6.0 server. We can
then duplicate that account on the SQL server, assign it appropriate
rights to the databases we're using (and specifically, the stored
procedures), and then use pass-through authentication.

I used the ASPNET account (which will cause problems later, but they're
interesting ones), though the account really doesn't matter (i.e. I did
<span style="FONT-WEIGHT: bold;">not</span> use this account on our
production server, but another one like it.) I think it's better to live
dangerously on development boxes, to catch problems early. Of course,
that's not all. In order for the account to be able to startup an
application pool, it has to be a member of the IIS\_WPG group. I didn't
find that anywhere in MSDN or the KB articles, but by experimentation.

So, pick an account, add it to the IIS\_WPG group, create an application
pool running under that account, duplicate that account on your SQL
server, set permissions to the databases and stored procedures desired.

Voila, right?

Problem \#2: You want to use the Enterprise Library Data Access
Application Block. So following the guidelines you write some code like
this:

<div class="cf">

Database authDB = DatabaseFactory.CreateDatabase("Authentication");

DBCommandWrapper dbCommandWrapper =
authDB.GetStoredProcCommandWrapper("usp\_LookupUserbyLoginID");

dbCommandWrapper.AddInParameter("@kerbID", System.Data.DbType.String,
requestUserID);

IDataReader reader = authDB.ExecuteReader(dbCommandWrapper);

<span class="cb1">bool</span> records = <span class="cb1">false</span>;

</div>

But get an error like this: <font size="+0"></span>

<font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0">
------------------------------------------------------------------------------------------------------------------------------------------------

*Security Exception*
--------------------

<font face="Arial, Helvetica, Geneva, SunSans-Regular, sans-serif ">**Description:**
The application attempted to perform an operation not allowed by the
security policy. To grant this application the required permission
please contact your system administrator or change the application's
trust level in the configuration file.  

**Exception Details:** System.Security.SecurityException: Requested
registry access is not allowed.  

**Source Error:**  


+--------------------------------------------------------------------------+
|     Line 157:    DBCommandWrapper dbCommandWrapper = authDB.GetStoredPro |
| cCommandWrapper("usp_LookupUserbyLoginID");                              |
|                                                                          |
|     Line 158:    dbCommandWrapper.AddInParameter("@kerbID", System.Data. |
| DbType.String, requestUserID);                                           |
|                                                                          |
|     Line 159:    IDataReader reader = authDB.ExecuteReader(dbCommandWrap |
| per);                                                                    |
|                                                                          |
|     Line 160:    bool records = false;                                   |
|                                                                          |
|     Line 161:                                                            |
|                                                                          |
| </code>                                                                  |
+--------------------------------------------------------------------------+


**<font face="Verdana">Source File:
</font>**\\\\Webdevel.caes.ucdavis.edu\\wwwroot\$\\EligibilityList\\AuthenticationModule.cs**<font face="Verdana">
   Line: </font>**159  

**<font face="Verdana">Stack Trace:</font>**  


+--------------------------------------------------------------------------+
|     [SecurityException: Requested registry access is not allowed.]       |
|                                                                          |
|        Microsoft.Win32.RegistryKey.OpenSubKey(String name, Boolean writa |
| ble) +473                                                                |
|                                                                          |
|        System.Diagnostics.EventLog.CreateEventSource(String source, Stri |
| ng logName, String machineName, Boolean useMutex) +443                   |
|                                                                          |
|        System.Diagnostics.EventLog.WriteEntry(String message, EventLogEn |
| tryType type, Int32 eventID, Int16 category, Byte[] rawData) +347        |
|                                                                          |
|        System.Diagnostics.EventLog.WriteEntry(String message, EventLogEn |
| tryType type, Int32 eventID, Int16 category) +21                         |
|                                                                          |
|        System.Diagnostics.EventLog.WriteEntry(String message, EventLogEn |
| tryType type, Int32 eventID) +15                                         |
|                                                                          |
|        Microsoft.Practices.EnterpriseLibrary.Common.Instrumentation.Even |
| tLogger.Log(String message)                                              |
|                                                                          |
| </code>                                                                  |
+--------------------------------------------------------------------------+

</font></i><span style="FONT-FAMILY: Arial,Helvetica,Geneva,SunSans-Regular,sans-serif;"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><font size="+0"><!--StartFragment -->

</h2>
</span></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font></font><font size="2"><font face="Arial">If
you look at the Stack Trace, you can see the problem is with the
CreateEventSource() call. Even though you haven’t specified using the
Enterprise Library Logging Block, secretly it is still using
System.Diagnostics.EventLog as part of its setup.</font></font>

<font size="2"><font face="Arial">Here’s an article which describes the
problem:</font></font>

<font size="2"><font face="Arial">[PRB: “Requested Registry Access Is
Not Allowed” Error Message When ASP.NET Application Tries to Write New
EventSource in the
EventLog](http://support.microsoft.com/default.aspx?scid=kb;en-us;329291)</font></font>

<font size="2"><font face="Arial">Unfortunately, the solutions don’t
work. Solution \#1, manually entering a registry key, didn’t work for
me. Solution \#2, writing some code which calls CreateEventSource() also
doesn’t *quite* work either.</font></font>

<font size="2"><font face="Arial">I say *quite* because the issue is
that CreateEventSource() needs to be called by a user with
Administrative Rights. So what I did was create a project using my
ErrorHandler class (from [Fun with Microsoft’s Enterprise
Library](http://acgetchell.blogspot.com/2005/02/fun-with-microsofts-enterprise-library.html)),
setup the project to run in App Pool \#1 which runs using the ASPNET
account, grant that account Admin rights, do iisreset && gpupdate
/force, open the project’s default web form thereby causing an event to
be written which calls the ErrorHandler class which calls
CreateEventSource(), and then go back and revoke admin rights on
ASPNET.</font></font>

<font size="2"><font face="Arial">Unfortunately, this needs to be done
for every application which will call CreateEventSource() — unless you
want to leave ASPNET running as Administrator (**very bad
idea!**).</font></font>

<font size="2"><font face="Arial">Inelegant, but it works. I’ve notified
Microsoft KB site of my findings; perhaps they’ll revise the article, or
show something more elegant.</font></font>

Update: <font face="Arial" size="2">This is also discussed in the
[Enterprise Library
FAQ](http://www.gotdotnet.com/workspaces/customization/uploadedhtmlpage.aspx?FileID=ded67339-a081-489a-8d63-817323f31104&id=295a464a-6072-4e25-94e2-91be63527327).
However, the solutions given there are 1) run the “Install Services”
script (why would you install Visual Studio on a server?) 2) use
installutil on the EL assemblies (perhaps that will work — I’ll have to
try it) or 3) remove all logging from the EL (which in my case I
want).</font>

<font size="2"><font face="Arial">Okay, we’ve got that problem taken
care of. We write our EL application and breathlessly open the default
page, only to find:</font></font>

<font face="Arial" size="2"><!--StartFragment --><font face="Times New Roman" size="3"> Server
Error in '/EligibilityList' Application.  
--------------------------------------------------------------------------------  

File or assembly name ko20f8cc.dll, or one of its dependencies, was not
found.  
Description: An unhandled exception occurred during the execution of the
current web request. Please review the stack trace for more information
about the error and where it originated in the code.  

Exception Details: System.IO.FileNotFoundException: File or assembly
name ko20f8cc.dll, or one of its dependencies, was not found.  

Source Error:  


Line 119:      private bool Authorize(string requestUserID)  
Line 120:      {  
Line 121:         Database authDB =
DatabaseFactory.CreateDatabase("Authentication");  
Line 122://         IDataReader dataReader;  
Line 123:         DBCommandWrapper dbCommandWrapper =
authDB.GetStoredProcCommandWrapper("usp\_LookupUserbyLoginID", new
SqlParameter("@kerbID", requestUserID)); </font>  
</font>

<font face="Arial" size="2">This was discussed in the
[GotDotNet](http://www.gotdotnet.com/workspaces/messageboard/thread.aspx?id=295a464a-6072-4e25-94e2-91be63527327&threadid=ee840b95-2fb0-49c9-b888-26abd8268b98)
forums. The problem is this:</font>

<font face="Arial" size="2">[Process and request identity in
ASP.NET](http://support.microsoft.com/default.aspx?scid=317012)</font>

<font face="Arial" size="2">Behind the scenes the DAAB calls
XmlSerializer, which want to write a temporary assembly to run. ASPNET
(or the account you’re running under) doesn’t have access to the default
temp directory, C:\\Windows\\temp, so the assembly can’t be written and
the DAAB halts. Nice.</font>

<font face="Arial" size="2">To fix this, give the account the
Application Pool runs under **Full** (that’s right, it needs to create
subdirectories) permissions to C:\\Windows\\temp.</font>

<font face="Arial" size="2">By the way, this use of XmlSerializer has
[performance
implications](http://www.gotdotnet.com/workspaces/messageboard/thread.aspx?id=295a464a-6072-4e25-94e2-91be63527327&threadid=528cc244-f686-458f-b837-c5e319995087).

</font>

<font size="2"><font face="Arial">Finally, Enterprise Library is
installed, our code references it correctly, temporary assemblies can be
written locally, life is good.</font></font>

<font size="2"><font face="Arial">Then we install Windows Server 2003
Service Pack 1.</font></font>

<font size="2"><font face="Arial">And instantly, our web pages return
the very lonely:</font></font>

<font size="2">

<font face="Arial">Service Unavailable</font>
=============================================

<font face="Arial">Looking at IIS Manager, you can see that the
Application Pool has been disabled. Looking in the System Log from Event
Viewer shows this:</font>

<font size="1">

<font face="Arial">A failure was encountered while launching the process
serving application pool 'AppPool \#1'. The application pool has been
disabled.</font>

<font face="Arial">For more information, see Help and Support Center at
</font>[<font face="Arial">http://go.microsoft.com/fwlink/events.asp</font>](http://go.microsoft.com/fwlink/events.asp)<font face="Arial">.</font>

<font face="Arial" size="2">Of course that link leads to no further
information.</font>

<font face="Arial" size="2">To cut to the chase, the problem is that
Windows Server 2003 SP1 has revoked rights/permissions on the ASPNET
account, that cannot be restored even by placing it in the
Administrators group. The way to fix the problem is:</font>

<font face="Arial" size="2">Go to the .NET Framework Folder (typically
c:\\Windows\\Microsoft.NET\\Framework\\v1.1.4322)</font>

<font face="Arial" size="2">aspnet\_regiis -ua to uninstall the
framework</font>

<font face="Arial" size="2">aspnet\_regiis -i to reinstall the
framework</font>

<font face="Arial" size="2">In IIS Manager:</font>

<font face="Arial" size="2">Enable ASP.NET pages</font>

<font face="Arial" size="2">In User manager (compmgmt.msc)</font>

<font face="Arial" size="2">Set the ASPNET account with the password on
the SQL server, and as a member of IIS\_WPG</font>

<font face="Arial" size="2">In IIS Manager:</font>

<font face="Arial" size="2">Set the Application pool to run under the
account with the password entered from the previous step</font>

<font face="Arial" size="2">At the Run command:</font>

<font face="Arial" size="2">iisreset to reset IIS</font>

<font face="Arial" size="2">gpupdate /force to ensure password
synchronization</font>

**<font face="Arial" size="4">Wasn’t that fun?</font>**

<font face="Arial" size="2">Thank goodness Whidbey and Enterprise
Library v2.0 aren’t coming out until September.</font>

</font></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></font>

</p>
