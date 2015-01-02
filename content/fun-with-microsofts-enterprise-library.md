Title: Fun with Microsoft's Enterprise Library
Date: 2007-09-22 23:42
Author: Adam Getchell
Tags: .net
Slug: fun-with-microsofts-enterprise-library
Category: Programming

Oh yeah, back to my day-job: I'm a programmer.  

So we've got a new application to update the current stone-tablet
process in the University that determines if students actually
graduate.  

Now, I like to write good code, and furthermore, if someone else writes
it for me, that's even better. So if you are working on the .NET
platform, you'd do well to look at the [Enterprise
Library](http://www.microsoft.com/downloads/details.aspx?FamilyId=0325B97A-9534-4349-8038-D56B38EC394C&displaylang=en).  

Of course, this is several thousand lines of code to pore over, good
stuff, but unfortunately we have these minor annoying things called
deadlines which prevents us from taking the time to grok everything
properly.  

Come to think of it, this happens in Physics, too -- I never have enough
time to actually understand all the details of the problems I'm supposed
to be solving, but my advisor assures me that this is the proper state
of things in research, as opposed to writing text books, and three
guesses as to which one gets you tenure.  

Back to the matter at hand -- the Enterprise Library. Looking around at
some good [working
examples](http://blog.hishambaz.com/archive/2005/01/29/194.aspx) ,
hilarity and pandemonium ensues when you try to do something simple like
write to the Event Log when your application barfs. (Did I mention this
doesn't come up a lot because instrumenting software seems to be a ...
novelty?) I'm pretty sure that developers should <span
style="font-weight: bold;">not</span> be doing things like editing the
Registry, installing Services, or setting accounts programs run under
with full admin rights -- I was a system administrator in a previous
job, and I <span style="font-weight: bold;">hated</span> letting
programmers do those kind of things.  

So I won't inflict the same damage on our own, long-suffering sysadmin.  

Now, my 52-line class solution doesn't do all the bells and whistles the
EL does, but it sure doesn't require all the nastiness above:  


<div class="cf">

<span class="cb1">using</span> System;

<span class="cb1">using</span> System.Diagnostics;

 

<span class="cb1">namespace</span> CAESDO

{

    <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\<summary\></span>

    <span class="cb2">///</span><span class="cb3"> Methods to handle
error reporting</span>

    <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\</summary\></span>

    <span class="cb1">public</span> <span class="cb1">class</span>
ErrorHandler

    {

        <span class="cb1">public</span> ErrorHandler()

        {

            <span class="cb3">// Register application as source for
Application log</span>

            <span class="cb1">if</span>
(!EventLog.SourceExists("FacultyStudentSurveys"))

                EventLog.CreateEventSource("FacultyStudentSurveys",
"Application");

        }

 

        <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\<summary\></span>

        <span class="cb2">///</span><span class="cb3"> Writes an error
message to the Application Event Log</span>

        <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\</summary\></span>

        <span class="cb2">///</span><span class="cb3"></span><span
class="cb2">\<param name="error"\></span><span class="cb3">The thrown
exception</span><span class="cb2">\</param\></span>

        <span class="cb1">internal</span> <span class="cb1">void</span>
WriteToEventLog(Exception error)

        {

            <span class="cb1">const</span> <span
class="cb1">string</span> source = "Commencement";

            <span class="cb1">const</span> <span
class="cb1">string</span> logName = "Application";

            EventLogEntryType enumType = EventLogEntryType.Error;

 

            EventLog objectLog = <span class="cb1">new</span>
EventLog(logName);

            objectLog.Source = source;

            objectLog.WriteEntry(error.Message, enumType, 1 );

        }

 

        <span class="cb1">internal</span> <span class="cb1">void</span>
WriteToEventLog(<span class="cb1">string</span> message, <span
class="cb1">bool</span> success)

        {

            <span class="cb1">const</span> <span
class="cb1">string</span> source = "Commencement";

            <span class="cb1">const</span> <span
class="cb1">string</span> logName = "Application";

            EventLogEntryType enumType;

 

            <span class="cb1">if</span> (success)

            {

                enumType = EventLogEntryType.Information;

            }

            <span class="cb1">else</span>

            {

                enumType = EventLogEntryType.Error;

            }

            EventLog objectLog = <span class="cb1">new</span>
EventLog(logName);

            objectLog.Source = source;

            objectLog.WriteEntry(message, enumType);

        }

    }

}

</div>



I'm sure I've missed something obvious. Anyone?  

I just got a reply from the Hisam Baz, author of the above weblog which
says, "Why write 52 lines of code when you can write 1?".  

To which I reply, "I'd be happy to write 1 line of code -- if it
works."  

Which brings us to the second problem:  

<span style="font-weight: bold;">Non-portable references to the Global
Assembly Cache in ASP.NET</span>  

Once you actually try to use the Enterprise Library, you'll often come
across this bit of advice:  

"<span style="font-weight: bold; font-style: italic;">References  

</span><span style="font-style: italic;">Then from your application, add
references to
Microsoft.Practices.EnterpriseLibrary.Configuration.dll</span>  
<span style="font-style: italic;">and
Microsoft.Practices.EnterpriseLibrary.Logging.dll from the C:\\Program
Files\\Microsoft Enterprise Library\\bin\\ directory. You should
consider signing the assemblies and then adding them to the GAC. You
should also add a copy of the assemblies to C:\\Program Files\\Microsoft
Visual Studio .NET 2003\\Common7\\IDE. Once you do that, you can select
the assemblies directly from the "Add Reference" dialog. One you've
added the reference, then add the appropriate using statement - using
Microsoft.Practices.EnterpriseLibrary.Logging - to your code."</span>  

There's only one problem -- it doesn't work.  

1. When Visual Studio 2003 .NET looks for references in the Global
Assembly Cache, it never updates its view of the GAC in response to what
you've added -- that's done by the
[registry](http://support.microsoft.com/default.aspx?scid=kb;en-us;306149)
(bleah). Which is why you've got to add a copy where VS can find it.  

2. When writing ASP.NET applications, references should be against
assemblies in the webserver GAC. And naturally, installer projects
written in VS 2003 do not install the files in the GAC automatically, as
they do for the web application itself. So now you have to manually add
assemblies to the GAC and write registry entries for each assembly to be
resolved by the .NET runtime.  

Wait, why are we [using the
GAC](http://www.sellsbrothers.com/news/showTopic.aspx?ixTopic=1199)
again?  

Okay, looks like I'll have to wade through [Richard Grime's Fusion
Workshop](http://www.grimes.demon.co.uk/workshops/fusionWS.htm). Except
that it doesn't cover the case I'm interested in. Joy.  

Well, I sure hope that the 10 lines of code I'll end up emitting in this
exercise will exceed the several thousand I could be writing if I just
wrote everything myself.  

What's that again about the virtues of programmers? Laziness,
impatience, and hubris. Oh, alright then.

</p>
