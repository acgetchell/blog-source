Title: Iterations
Date: 2013-12-07 18:56:50 -0800
Tags: macos, c++, octopress, prismbreak, bjj

It's been quite awhile since the last post, with lots of changes. I've:

- Converted to MacOS
- Changed my research codebase to C++
- Migrated this blog from Blogger to Octopress
- Started on the path towards [#prismbreak][1]
- Gotten my blue belt in BJJ

I'll say a little about each of these in turn.

<!--more-->

MacOS++
-------
First, for scientific research MacOS < (Windows)++.

I've tried both, I simply get more done in MacOS. Mainly, it's because there's generations of Unix tools I can still use in an honest bash shell. [Homesick][2] is simply lovely for managing your dotfiles, and [bash-it][3] is another awesome shell configuration management tool. I pretty much live in [GitHub][4] for anything public (research papers and code, presentations, work projects, and this blog) and with tools like [Homebrew][5] I can restore my development environment and files on any Mac I care to just by running a shell script.

Second, any large complex pieces of software that I find worth purchasing such as Mathematica, Maple, Office, MindNode Pro, Parallels, [SublimeText][6], or [1Password][7] already runs fine on MacOS. As do myriads of other useful free or open source tools such as (let me look at my Dock) [Chrome][8], [Tor][9], [DashDoc][10], [GitHub][11], [LightTable][12], [EverNote][13], [Zotero][14], [Anki][15], and [TrueCrypt][16]. And then there's the software Apple bundles such as XCode, iTunes, iMessage, iWork, iMovie, and Garage band. Let's not forget that any non-console games I care about work great on [Battle.Net][17] or [Steam][18]. Or that the AppStore keeps paid apps in the cloud, and Homebrew/Homesick keeps the rest. Finally, if there are any Windows tools I absolutely have to have such as [Visual Studio][19] or modern versions of Outlook, [Parallels][20] works dandy.

Now, putting on my IT hat for a moment, if you are in a corporate environment and don't care one whit about the command line, then Windows is the best for you. Or rather, you're probably indifferent (although you may want *teh shiny*), but for your tech staff, Windows machines can be managed by the thousands with relative ease. Microsoft actually supports doing so in an efficient business fashion. Apple simply doesn't care about the enterprise space, and [Google's][21] [toolkit][22] doesn't quite fill in the gaps (although I am sure that [Puppet][23] masters will disagree with me).

Also, if you live in [Azure][24] or Visual Studio or like the [Surface][25] hardware (and they are interesting) Windows has got it going (although some of us just buy Macs and load Windows, because the hardware is still [shiny][26]).

It goes without saying that if you're one of those folks that love rolling your own OS and hardware, Linux is for you. Most of us, I suspect, simply need to get things done. Hence the resurgence in MacOS share.

C++
---

Some of you may remember that I'm working on [quantum gravity][27]. Now it turns out that for the kinds of things I want to do -- construct simplicial manifolds by the thousands and manipulate their geometry to insert masses and other objects; then read off the various attributes of these spacetimes and the objects therein -- I am going very far down a very deep rabbit hole named [computational geometry][28].

But lo, there was light and illumination in the dark tunnels of my madness, and its name is [CGAL][29].

And CGAL is written in [C++][30].

(Oh, sure, there are [Python bindings][31] too. But they don't cover everything, and I haven't tested all of their functions.)

But now that I'm down one rabbit hole, I may as well continue, and I've found much to my surprise I am enjoying [re-learning][32] and using C++. Luckily for me, the C++11 standard is here, and C++ really does feel like another language. CGAL makes fundamental use of generic programming, and the toolchain has gotten better too. With CGAL, C++, [CMake][33], [Doxygen][34] and friends I am [literate-ly][35] [test-kinda-driven developing][36] my way for great good.

[Clojure][37] and [Lisp][38] are still lovely. But I can generate 5 million simplex complexes in 10-50 seconds on just my laptop, and if there ever was a need for speed and parallelization I have it. (Ah, [julia][39], you are a lovely language, Y U No compile on MacOS?) And maybe someday we'll have Quantum Gravity on your Desktop courtesy of [BOINC][40].

Octopress++
-----------

I [moved from Blogger][41] to [Octopress][42] for a number of reasons.

- Octopress is open source, works using git, and works well on GitHub. There are a ton of [plug-ins][43] and it's easy to write your own.
- I want to [reclaim my network identity][44], and a platform that I can regenerate anyplace with just a `git pull`
- Mirroring the move to C++, this blog is written very infrequently but read, well more often than it is written. So the overhead of a database and a dynamic site is not worth it.
- Did I mention it works in git and GitHub? I live there these days. And the [bash-it git aliases][45] rock!
- `rake preview` `rake generate` `rake deploy` then `gall` `gca` `gpo source` is a lovely workflow.
- Lot's of [resources][46] [to][47] [get][48] [going][49].


Prismbreak++
------------

We [all][50] [kinda][51] [knew][52] [it][53]. The internet is a vast info-trawl for almost anything, but especially [all the private info people are trading away for services][54]. Getting your own independent network identity is just the [first step][55], but there are many, many others (such as using [TrueCrypt][16] for any cloud file storage on any files you care to keep private). There are also quite a few inconviences; after all there's a reason folks use the privacy-invading "[free][54]" services, and no I don't want Linux for my primary laptop. I'll (possibly) have more to say on this later.

(If you *are* going to pick an operating system for privacy, the best choice is [OpenBSD][56].)

Martial Arts++
--------------

I've been practicing martial arts of various types for quite awhile now. I'm fairly highly ranked in a few.

But the empirical evidence is in, and it is this:

To fight effectively, you need awareness, strength, quickness, toughness, calmness, cardio, and a whole host of attributes often listed on RPG sheets. To which skill in striking, grappling, and on the ground are musts.

I love Taekwondo and it's spin kicks, but I am not deluding myself. You simply don't learn to deal with most other forms of striking. You will have beautiful kicks, but someone with a few months of boxing will punch you in the face quite easily. And of course, any type of grappler that closes the distance (or, anytime you miss) will grab hold of you to your detriment.

I learned Judo and love the throws, but I'd rate it below Wrestling and Sambo in effectiveness. Primarily due to the new rules changes which forbid wrestling-style double and single leg takedowns.

And on the ground, of course, Brazilian Jiu-Jitsu is king.

All of these statements are pretty easily tested. You can personally test it by going to boxing clubs, wrestling workouts, and BJJ gyms and see how you fare in these areas. Or you can just watch UFC and see professionals do the same.

And if you object that all of these places have rules, and aren't a real fight: please tell me why you think various dirty tricks will win the day for you, especially when you're in an inferior position where your opponent can do the same back to you (but 10x worse).

I teach Hapkido at the university, and I've always enjoyed that Hapkidoja *did* learn techniques in all of these areas. I competed in Taekwondo and Judo, and Hapkido synthesized them all together. It was good for practical self-defense. I try to teach it as such.

(Yes, martial arts with sporting equivalents are superior. Nothing beats realistic practice.)

But times change and things develop, and it's time to adapt and learn what works. And my [BJJ academy][57], [professor][58], and jiu-jitsu family rock!

Also, competing in BJJ is scary fun!

[1]: https://app.net/search/?type=posts&q=%23prismbreak
[2]: https://github.com/technicalpickles/homesick
[3]: https://github.com/revans/bash-it
[4]: https://github.com/acgetchell
[5]: https://github.com/mxcl/homebrew
[6]: http://www.sublimetext.com
[7]: https://agilebits.com/onepassword
[8]: https://www.google.com/intl/en/chrome/browser/
[9]: https://www.torproject.org
[10]: http://kapeli.com/dash
[11]: http://mac.github.com
[12]: http://www.lighttable.com
[13]: https://evernote.com
[14]: https://www.zotero.org
[15]: http://ankisrs.net
[16]: http://www.truecrypt.org
[17]: http://us.battle.net/en/
[18]: http://store.steampowered.com
[19]: http://www.visualstudio.com
[20]: http://www.parallels.com
[21]: https://www.usenix.org/conference/lisa13/managing-macs-google-scale
[22]: https://code.google.com/p/google-macops/
[23]: https://puppetlabs.com
[24]: http://www.windowsazure.com/en-us/
[25]: http://www.microsoft.com/surface/en-us
[26]: http://www.apple.com/mac/
[27]: http://arxiv.org/abs/hep-th/0105267
[28]: http://en.wikipedia.org/wiki/Computational_geometry
[29]: http://www.cgal.org
[30]: http://isocpp.org
[31]: https://code.google.com/p/cgal-bindings/
[32]: http://www.cprogramming.com
[33]: http://www.cmake.org
[34]: http://www.stack.nl/~dimitri/doxygen/
[35]: http://www.literateprogramming.com
[36]: http://pragprog.com/book/lotdd/modern-c-programming-with-test-driven-development
[37]: http://clojure.org
[38]: http://www.sbcl.org
[39]: http://julialang.org
[40]: http://boinc.berkeley.edu
[41]: http://toamitkumar.com/blog/2012/04/19/migrate-from-blogger-to-octopress-step-by-step-guide/
[42]: http://octopress.org
[43]: http://octopress.org/docs/plugins/
[44]: https://eschnou.com/entry/implementing-prism-break-62-25013.html
[45]: https://github.com/revans/bash-it/blob/master/aliases/available/git.aliases.bash
[46]: http://www.lucypark.kr/blog/2013/02/25/mathjax-kramdown-and-octopress/
[47]: http://jekyllrb.com
[48]: https://github.com/robertkowalski/octopress-coderwall
[49]: http://asaf.github.io/blog/2013/07/08/blogging-with-octopress-add-about-page/
[50]: https://www.aclu.org/technology-and-liberty/internet-privacy
[51]: https://www.eff.org/nsa-spying
[52]: http://www.foxnews.com/politics/2013/11/19/docs-say-nsa-repeatedly-assured-court-it-would-stop-surveillance-rules
[53]: http://www.wired.com/threatlevel/2012/03/ff_nsadatacenter/
[54]: http://lifehacker.com/5697167/if-youre-not-paying-for-it-youre-the-product
[55]: https://prism-break.org
[56]: http://www.openbsd.org
[57]: http://fabiopradobjj.com
[58]: http://fabiopradobjj.com/about-fabio-prad0/
