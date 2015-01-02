Title: Reflection tools for F#
Date: 2011-04-19 08:52
Author: Adam Getchell (noreply@blogger.com)
Tags: f#
Slug: embedding-gists-in-blogger
Category: Programming

I went to the fabuluous [CodeConf 2011](http://codeconf.com/) (view
[slides](http://lanyrd.com/2011/codeconf/slides/),
[recaps](https://github.com/blog/835-codeconf-2011-mission-accomplished)
[here](http://www.peebs.org/2011/04/codeconf-2011-day-one/),
[here](http://thechangelog.com/post/4507882708/codeconf-sunday-summary),
and [here](https://convore.com/codeconf/)) and the first talk was
"Tinker Fairy" [Dr. Nic](http://twitter.com/#!/drnic) telling us to
[build tools](http://lanyrd.com/2011/codeconf/sdmxb/) to do stuff that
we don't want to remember later. Then build tools to build those
tools -- tool tools.  

One of the neat modern takes on Lisp
[s-expressions](http://en.wikipedia.org/wiki/S-expression) in modern
virtual machines like the CLR is
[Reflection](http://en.wikipedia.org/wiki/Reflection_(computer_programming)).
At least, I think that it will be useful in reversing Lisp macros and
expressions into the F\#/OCAML equivalents.  

[Dr. Jon Harrop](http://flyingfrogblog.blogspot.com/) gives a terse but
informative example in his book [Visual F\# 2010 for Technical
Computing](http://fsharpnews.blogspot.com/2010/04/visual-f-2010-for-technical-computing.html).  

First, we want a union type which represents (i.e. abstracts away) the
F\# type system:  



Next, we want a (recursive) function (called, straightforwardly enough,
type\_of) that reflects (using FSharpType) and translates a given
System.Type object into one of the 'a ty union types defined
previously:  



This then allows us to emit the following two liner which can parse
objects such as the List.fold function! (Note: everything after the ;;
is the F\# Interactive response.)  



Neat stuff! I've a thousand or two lines of Lisp to look at, so this is
not something I want to have to remember later.
