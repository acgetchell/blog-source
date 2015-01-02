Title: Microsoft Security Awareness training
Date: 2007-09-22 23:41
Author: Adam Getchell (noreply@blogger.com)
Tags: openbsd
Slug: microsoft-security-awareness-training

[This](http://www.atrevido.net/blog/PermaLink.aspx?guid=256b6bb4-f6f4-43a5-985b-7fe5796b809c)
is just too funny to pass up.  
  
So far, [malware's winning the war of
attrition](http://windowssecrets.com/050127/#story1).  
  
Well, at least [Microsoft
Anti-Spyware](http://www.microsoft.com/athome/security/spyware/software/default.mspx)
is going to be free.  
  
Too bad there's already [malware which targets
it](http://www.pcworld.com/resource/article/0,aid,119641,pg,1,RSS,RSS,00.asp).  
  
You do have a real hardware firewall, don't you? If not, there's no
reason why you shouldn't -- here's my [OpenBSD
recipe](http://insecure.ucdavis.edu/OpenBSD/openbrick) that works
beautifully on inexpensive hardware, and has big-bucks features like
stateful filtering, source tracking, bandwidth queuing, NAT, OS
detection, adaptive state table timeouts, MAC address tagging (with
brconfig), macros and tables, and hardware failover capability. All for
the price of an [OpenBSD CD](http://www.openbsd.org/orders.html) and
whatever hardware you run it on.  
  
(One of the firewalls I set up for a class C network was a Pentium 166
with 32MB of RAM, and it mostly sat at 99% idle filtering a 100MB
full-duplex LAN. OpenBSD has a very efficient network stack. When I've
gone around to help setup OpenBSD firewalls for departments at UC Davis,
we mostly recycle leftover desktops that have been replaced.)  
  
Of course, to help deal with malware you'll also have to do egress
filtering (not just ingress filtering, where most rulesets stop), and as
always, keep your systems patched.  
  
But then, there's no such thing as a panacea.  
  
Did I also mention that pf rules are nearly plain-language?  
  
[pf](http://www.openbsd.org/faq/pf/index.html) r0x0rs!
