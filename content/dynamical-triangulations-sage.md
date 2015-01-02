Title: Dynamical Triangulations, SAGE
Date: 2007-12-10 19:09
Author: Adam Getchell (noreply@blogger.com)
Tags: SAGE, quantum gravity, python, vmware, ubuntu
Slug: dynamical-triangulations-sage
Category: Physics

The first paper I read for Causal Dynamical Triangulations is a fairly
steep introduction (for me), so I went and looked over the
[2D](http://arxiv.org/abs/hep-th/9805108) case and
[lessons](http://arxiv.org/abs/hep-th/9806241), as well as a general
[review](http://relativity.livingreviews.org/Articles/lrr-1998-13/) of
methods.  

I'm also looking at [SAGE](http://www.sagemath.org/), Software for
Algebra and Geometry Experimentation, a free mathematical programming
system using [Python](http://www.python.org/) + a lot of open source
tools. On Windows, SAGE
[requires](http://www.sagemath.org/SAGEbin/microsoft_windows/README.txt)
[VMWare](http://www.vmware.com/products/player/) and uses firefox. You
can use it [online](https://sage.math.washington.edu:8103/login), but so
far it's rather slow, and appears to have been
[slashdotted](http://science.slashdot.org/science/07/12/08/1350258.shtml).  

Impressive tool! Feels a lot like Mathematica, accessible via web
browser. The
[tutorial](http://modular.math.washington.edu/sage/doc/html/tut/tut.html)
is well-worth running through (I used the on-line version while
upgrading my local install, but the local version allows you to run the
calculation cells using Shift-Enter ).  

For example, SAGE extends Python to handle
[rings](http://en.wikipedia.org/wiki/Ring_%28mathematics%29) and
[p-adic](http://en.wikipedia.org/wiki/P-adic_number) numbers (which I
learned, should always have a prime number base to avoid the
zero-divisor problem).  

Adding dvipng SAGE package requires adding ghostscript, via apt-get
install gs.  
Also requires libkpathsea, which requires tetex via apt-get install
tetex-extra  

PostScript: the SAGE dvipng package doesn't work, but apt-get install
dvipng puts dvipng on the system, which should suffice.  

Note: SAGE runs on Edgy, and can be updated to Feisty by using
update-manager-core as described
[here](http://www.ubuntu.com/getubuntu/upgrading). The
[SAGE-support](http://groups.google.com/group/sage-support) group is
available on Google Groups.  

PostScript: SAGE can be upgraded to Gutsy, I used the Upgrade Manager
available in Xubuntu (I wanted a GUI for some SAGE file management via
apt-get install xubuntu-desktop)  

Doesn't work yet on BSD, alas, and running a SAGE server has security
implications.
