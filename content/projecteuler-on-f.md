Title: ProjectEuler on F#
Date: 2007-11-19 09:24
Author: Adam Getchell
Tags: .net, f#
Slug: projecteuler-on-f
Category: Programming

So, whilst poring through Pickering's book and browsing through [Tomas
Petricek's blog](http://tomasp.net/about/fsharp.aspx) (which has a
promising [F\# AJAX
toolkit](http://tomasp.net/articles/fswebtools-intro.aspx), which alas,
doesn't work yet) and stealing glances at the [O'Reilly online OCAML
book](http://caml.inria.fr/pub/docs/oreilly-book/html/index.html), I
decided to write some programs to exercise my understanding of the
material. After some stumbling, I found [Project
Euler](http://projecteuler.net/index.php?section=problems), a great site
full of math programming puzzles.  

I solved [Problem
\#1](http://projecteuler.net/index.php?section=problems&id=1) naively in
\~ 10 lines of F\# using list comprehensions and recursion (I've seen a
one-liner using Seq.fold). [Problem
\#2](http://projecteuler.net/index.php?section=problems&id=2) builds on
this and takes about 30, including a debugging function to print results
([better
solutions](http://blogs.msdn.com/chrsmith/archive/2007/10/26/Project-Euler-in-F_2300_-_2D00_-Problem-2.aspx),
using Seq.unfold, do it in 10). I posted my code solutions to the
[forum](http://projecteuler.net/index.php?section=forum), so as not to
spoil anyone else's fun (you can only post to the forum for that problem
after you've solved it). It's very interesting to see all of the other
solutions in different languages, and the algorithm discussion is
fascinating too.  

It's also quite impressive how easily F\# morphs into math problems
(though I am still writing some horrid C\#/F\# hybrid presently).  

Oh, and here's a nifty 100-line podcast downloader,
[slurppodcasts](http://dcooney.com/ViewEntry.aspx?ID=499).  

(Note that <span style="color: rgb(51, 51, 255);">Idioms.using</span> is
no longer necessary, since <span
style="color: rgb(51, 51, 255);">using</span> is integrated into F\#)  

Finally, here's [Feedburner's Planet
F\#](http://feeds.feedburner.com/planet_fsharp).
