Title: Causal Dynamical Triangulations
Date: 2008-08-01 08:33
Author: Adam Getchell
Tags: quantum gravity, vmware, ubuntu, cdt
Slug: causal-dynamical-triangulations
Category: Physics

Rajesh Kommu and [Professor Steve
Carlip](http://www.physics.ucdavis.edu/Text/Carlip.html) are working on
interesting ways to model quantum gravity using computational methods.
Rajesh has been kind enough to help show me where to get started:  

[Dynamically Triangulating Lorentzian Quantum
Gravity](http://arxiv.org/PS_cache/hep-th/pdf/0105/0105267v1.pdf)  

[A non-perturbative Lorentzian path integral for
gravity](http://arxiv.org/PS_cache/hep-th/pdf/0002/0002050v3.pdf)  

[Non-perturbative 3d Lorentzian Quantum
Gravity](http://arxiv.org/PS_cache/hep-th/pdf/0011/0011276v2.pdf)  

[Spectral Dimension of the
Universe](http://arxiv.org/PS_cache/hep-th/pdf/0505/0505113v2.pdf)  

As things often do, it turns into code, which Rajesh has again
provided.  

Of course, Visual Studio 2008 Beta 2 has some ... issues with the
[STL](http://blogs.msdn.com/vcblog/archive/2006/08/02/686894.aspx).  

So, in the interest of getting working code I'll try a virtual instance
of Ubuntu which I should be able to
[upgrade](http://www.ubuntu.com/getubuntu/upgrading) later when 7.10
comes out later this month).  

[VMWare](http://register.vmware.com/content/download.html) server
requires IIS7, so here's the instructions for [installing IIS7 on
Vista](http://www.iis.net/articles/view.aspx/IIS7/Deploy-an-IIS7-Server/Installing-IIS7/Install-IIS7-on-Vista).  

Except that I couldn't connect to my own VMWare server, and apparently
[VMWare has issues on
Vista](http://weblogs.asp.net/kdente/archive/2007/03/14/vmware-on-vista-lameness.aspx)
... sigh.  

Okay, it seems to be a [driver signing
issue](http://communities.vmware.com/docs/DOC-1375).  

Meh ... [Virtual PC
2007](http://www.microsoft.com/windows/products/winfamily/virtualpc/default.mspx)
will probably suffice for my purposes. I'll keep IIS7.0 anyways for when
I install Visual Studio 2008 Release Candidate and want to develop
against IIS.  

... Except that Virtual PC 2007 apparently doesn't know how to handle
Ubuntu. Just hangs at the nice pretty install screen, wasting CPU
cycles.  

Back to VMWare server. Looks like I can disable driver signing
permanently using an admin console:  

<span style="font-family: courier new;">bcdedit.exe /set
nointegritychecks ON  
bcdedit -set loadoptions \\DISABLE\_INTEGRITY\_CHECKS  

</span>Let's try this again.  

Hmmm, that \*still\* didn't disable driver signing. So, bootup using F8,
disable driver signing.  

Now install VMWare Server 1.04. This time, I'll pick a slimmer linux
distribution, like [Xubuntu](http://www.xubuntu.org/).  

I have to admit, nice, slick, easy install. Not as fast as
[OpenBSD](http://www.openbsd.org/)'s bare-bones, efficient text setup,
but it's pretty, and more importantly, it works (unlike the heavier
Ubuntu desktop I just tried).  

Now install VMTools. Oh, it's an rpm. Fortunately, there are ways to
[install using an RPM
file](https://ubuntu.wordpress.com/2005/09/23/installing-using-an-rpm-file/).  

Hmmm. Should I be surprised that this didn't work? Okay, back to
installing a tarball.  

That worked, even though it also overwrote pre-existing stuff from the
RPM.  

Actually, no it didn't. It just stopped VMWare from nagging that VMTools
isn't installed. I'll just deal with the mouse capture for now, because
this really all is besides the point. (Note to self: more empathy for
people just trying to get their work done using computers.)  

Some things never change. Xubuntu has 84 updates to patch!  

Well, the whole point of this was to compile this under Linux (where
Rajesh wrote it) instead of tailchasing Visual Studio 2008/C++ STL
issues. Almost there! Now to find a decent IDE.  

I've heard good things about Eclipse, but I don't really want to [unpack
Java, install Tomcat, Web
Tools](https://help.ubuntu.com/community/EclipseWebTools), etc. etc.
when I don't plan to do any web development. I just want the C/C++
portion.  

Ah, [CDT](http://wiki.eclipse.org/index.php/CDT) looks like what I want.
Is the magic incantation really:  

<span style="font-family: courier new;">\# sudo apt-get
install</span>[<span
style="font-family: courier new;">eclipse-cdt</span>](http://packages.ubuntu.com/edgy-backports/devel/eclipse-cdt)<span
style="font-family: courier new;">  
\# sudo apt-get install eclipse</span>  

Wow, looks like it is! Now to see if Rajesh' CDT code compiles ....  

Okay, right now Eclipse is a tad confusing. And again, learning Eclipse
isn't the point.  

Let's go back to that old standby, vi.  

Sure helps to have a c++ compiler installed  

<span style="font-family: courier new;">\# sudo apt-get install
g++</span>  

Well, okay, looks like I'm missing some other files. Make doesn't know
how to make cdtworks. A structural issue.  

So, when something fails, try something else ...  

Made some more progress on the Windows VC++ 9 version. Turns out, even
though the project files were stored in my C:\\Projects file, Visual
Studio had other ideas, and expected everything to be stored in the
Visual Studio default file path. I'll just leave that one, since the
default file path ends up getting stored on our SAN, whereas I've had
the most lovely fun with hard drives and Bitlocker (which is again,
besides the point).  

Almost complies, although VC++ wants all header file declarations in
stdfx.h. Just missing one file ... again!  

On the other hand, now I can read code in two OSes. Sure is interesting
dereferencing all those pointers!  

Quantizing spacetime is fun, though!
