Title: CDT rewrite toolbox
Date: 2010-01-20 07:54
Author: Adam Getchell
Tags: lisp, cdt, python
Slug: cdt-rewrite-toolbox
Category: Programming

So, my colleagues have developed a
[CDT](http://adamgetchell.blogspot.com/2007_10_01_archive.html) program
that's usable. Fortunately for me, it's in LISP, which lacks parallel
processing, modern libraries, a nice IDE, and the other goodies I've
become accustomed to in my work life. (That means I get to figure these
features out and thereby contribute!)  

Enter Visual Studio 2008, [IronPython](http://ironpython.codeplex.com/),
and [IronScheme](http://ironscheme.codeplex.com/).  

Setting up IronScheme with Visual Studio 2008 was usefully detailed
[here](http://ironscheme.codeplex.com/wikipage?title=IronScheme%20Visual%20Studio%202008%20Integration&referringTitle=Documentation):
(note, you need
[RegPkg](http://msdn.microsoft.com/en-us/library/bb707481.aspx) via the
[Visual Studio 2008
SDK](http://www.microsoft.com/downloads/details.aspx?familyid=30402623-93ca-479a-867c-04dc45164f5b&displaylang=en))  

Setting up IronPython with Visual Studio 2008 via [IronPython Studio
(integrated
setup)](http://ironpythonstudio.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=8934):  

And voila, no more excuses to complain about development.  

(Yes, the end goal is to make it Python and cross-platform, although I'm
really eying F\#)
