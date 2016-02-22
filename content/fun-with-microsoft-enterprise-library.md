Title: Fun with Microsoft Enterprise Library, part 2
Date: 2007-09-22 23:41
Author: Adam Getchell
Tags: .net
Slug: fun-with-microsoft-enterprise-library
Category: Programming

Okay, I can see that this is going to be a long series ....  

Here's what I'm talking about on how to get Visual Studio to see
Enterprise Library assemblies without browsing (taken from the GotDotNet
workspace patterns & practices: Enterprise Library: Message Boards):  

"<span style="font-style: italic;">Do you want to see EntLib assemblies
in Add References message box?</span>  
<span style="font-style: italic;">Create a text file named entlib.reg,
and add this content:</span>  
<span style="font-style: italic;">Windows Registry Editor Version
5.00</span>  

<span
style="font-style: italic;">[HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\VisualStudio\\7.1\\AssemblyFolders\\Enterprise
Library]</span>  
<span style="font-style: italic;">@="C:\\\\Program Files\\\\Microsoft
Enterprise Library\\\\bin\\\\"</span>  

<span style="font-style: italic;">Double click on the file and you'll be
asked whether to add this registry key. Click yes, restart vs.net and
there you go.</span>  
<span style="font-style: italic;">(it is assumed that assemblies are in
their default folder - otherwise, change the path above).</span>"  

Sigh. I really really try to avoid the Registry when possible.  

There's another neat trick for sorting out the structure of the
Enterprise Library: open one of the solutions in Visual Studio, select
Project-\> Visio UML -\> Reverse Engineer.  

Too bad all it actually does is generate a 75K blank Visio file, because
Visio is unable to resolve all of the references.  

I suppose this will work for code that's so simple that a UML diagram
isn't needed.  

Moving right along, I've also found how to sign all of the Enterprise
Library Asemblies! You just generate your public/private key pair, and
then reference them in the GlobalAssemblyInfo.cs file in:  

C:\\Program Files\\Microsoft Enterprise Library\\src  
This file gets referenced by every project when it's compiled. Yay!  

Except that every project's AssemblyInfo.cs contains blank references:  

[assembly : AssemblyDelaySign(false)]  
[assembly : AssemblyKeyFile("")]  
[assembly : AssemblyKeyName("")]  

Which overwrite what gets pulled in from GlobalAssemblyInfo.cs.  

So you have to go through every project's AssemblyInfo.cs file and
remove those 3 lines.  

Sigh. There's 23 projects in the Security section alone, which is sort
of the <span style="font-style: italic;">sine qua non</span>for using
the EL to begin with, for my purposes.  

Well, Caching, Configuration, Data, ExceptionHandling, and Logging are
also useful.  

One step at a time.  

I've gotten Logging to work. Unfortunately, every time it logs it throws
three error messages:  

<span class="messagecontent"><span style="font-style: italic;">"Failed
to create instances of performance counter 'Distributor: \# of Logs
Distributed/Sec' - The requested Performance Counter is not a custom
counter, it has to be initialized as ReadOnly..</span>  

<span style="font-style: italic;">For more information, see Help and
Support Center at http://go.microsoft.com/fwlink/events.asp."</span>  

<span style="font-style: italic;">"Failed to fire the WMI event
'LoggingLogWrittenEvent'. Exception: System.Exception: This schema for
this assembly has not been registered with WMI.</span>  
<span style="font-style: italic;">at
System.Management.Instrumentation.Instrumentation.Initialize(Assembly
assembly)</span>  
<span style="font-style: italic;">at
System.Management.Instrumentation.Instrumentation.GetInstrumentedAssembly(Assembly
assembly)</span>  
<span style="font-style: italic;">at
System.Management.Instrumentation.BaseEvent.Fire()</span>  
<span style="font-style: italic;">at
Microsoft.Practices.EnterpriseLibrary.Common.Instrumentation.InstrumentedEvent.FireWmiEventCore(BaseEvent
baseEvent).</span>  

<span style="font-style: italic;">For more information, see Help and
Support Center at http://go.microsoft.com/fwlink/events.asp."</span>  

and  

<span style="font-style: italic;">"Failed to create instances of
performance counter 'Client: \# of Logs Written/Sec' - The requested
Performance Counter is not a custom counter, it has to be initialized as
ReadOnly..</span>  

<span style="font-style: italic;">For more information, see Help and
Support Center at http://go.microsoft.com/fwlink/events.asp."</span>  

Presumably these counters are installed as part of the EL service
installation, but going through the batch file yields for logging:  

@ECHO.  
@ECHO ---------------------------------------------------------------------------------  
@ECHO Installing Services for the Logging and Instrumentation
Application Block  
@ECHO ---------------------------------------------------------------------------------  
@ECHO.  

if Exist Microsoft.Practices.EnterpriseLibrary.Logging.dll installutil
%1 Microsoft.Practices.EnterpriseLibrary.Logging.dll  
@if errorlevel 1 goto :error  

So I'd like to break out whatever counters are needed so I can install
them on the webserver, and ideally, be able to script this installation
for production code on a production server with an Installer project.  

Although I'm strongly tempted to just go back to using my ErrorHandling
class, which doesn't need anything installed anywhere.  

No, I'll persist in using the EL. I'm sure there will be a payoff --
like extending the Logging class to handle XML.  

Of course, to extend the EL one should be cognizant of all the Unit
Tests there built to ensure its continued functionality. So I need that
book on Test Driven Development real soon now.  

Well, at least I'm not bored.  
</span>
