Title: Software Archaeology
Date: 2011-04-11 22:19
Author: Adam Getchell
Tags:
Slug: software-archaeology
Category: Programming

[Vernor Vinge](http://en.wikipedia.org/wiki/Vernor_Vinge) prophetically
[wrote of a
time](http://books.slashdot.org/story/03/09/18/0411259/Review-A-Fire-Upon-the-Deep-Special-Edition)
when programmer-archaeologists maintained the fabric of civilization by
diving into and modifying legacy code which ran the systems that society
depended upon.

<div>



</div>

<div>

Various other folks have picked up on this notion, from the
[serious](http://java.sys-con.com/node/487614) to the
[humorous](http://giant-communist-robots.com/?p=154). Here, though, I'll
talk about this from my own perspective (which is what you came here
for, right?).

</div>

<div>



</div>

<div>

[Kernighan's](http://www.ieee.org/portal/cms_docs_societies/sscs/PrintEditions/200804.pdf)
saw goes that debugging code is twice as hard as writing it; therefore
we ought to keep our meaning clear and our code as simple as possible.
How to do so?

</div>

<div>



</div>

<div>

There are clear debates about that: [functional vs.
declarative](http://msdn.microsoft.com/en-us/library/bb669144.aspx),
[procedural vs.
object-oriented](http://www.virtuosimedia.com/dev/php/procedural-vs-object-oriented-programming-oop),
not to mention [Patterns &
Anti-Patterns](http://books.google.com/books?hl=en&lr=&id=HBAuixGMYWEC&oi=fnd&pg=PA383&dq=patterns+and+antipatterns&ots=emzw4QN8Dj&sig=AFOJ5TeY4zHfa1pCKky8ux_X9hQ#v=onepage&q=patterns%20and%20antipatterns&f=false),
[Dependency Injection/Loose
Coupling](http://martinfowler.com/articles/injection.html),
[Aspect-Oriented
Programming](http://en.wikipedia.org/wiki/Aspect-oriented_programming),
etc. etc. These can be very fun to get into and there are diverse and
subtle points all around, that I won't attempt to do them justice here
but if you've a free week or two read any of the above links and the
next five references thereafter and you'll come away more enlightened,
or more confused.

</div>

<div>



</div>

<div>

But in the meantime, you've either got to a) emit working code or b)
manage those who do a). And if you could do so without too badly
embarrassing yourself in the future (which is nigh impossible), or at
least, be willing to chalk them up as learning experiences, you're well
on your way to some sort of nirvana of ineffable, crystallized logic
which is a perfect solution to your problem.

</div>

<div>



</div>

<div>

(Getting a clear problem statement itself being at least half of the
battle and most of the difficulty, given business processes that aren't
well understood, or mutate depending upon who's doing them or in which
context. But that discussion more properly belongs in the realm of
project management and business analysis, and won't be further remarked
upon here.)

</div>

<div>



</div>

<div>

If you're not a coder yourself (or horribly out of date), you can still
make a fair crack at judging the product by the team. [The Mythical
Man-Month](http://www.amazon.com/Mythical-Man-Month-Software-Engineering-Anniversary/dp/0201835959)
is the canonical reference, but [Joel
Spolsky's](http://www.joelonsoftware.com/) [Joel
Test](http://www.joelonsoftware.com/articles/fog0000000043.html) is
pretty concise, descriptive, and useful.

</div>

<div>



</div>

<div>

Archaeology can imply adventurous, sunburned types digging around fossil
layers high in vast dusty mesas of stratified rock. And truth be told,
that's not a bad analogy for the cacophony of systems that the average
IT organization has inherited, cobbled together, purchased (often from a
now-defunct vendor), or perhaps in a fit of creativity -- produced.
After all, post dot-com, [Greenfield
development](http://footheory.com/blogs/donnfelker/archive/2008/05/05/software-development-greeenfield-vs-brownfield.aspx)
is rare.

</div>

<div>



</div>

<div>

But Brownfield development is often so painful that most developers will
throw up their hands and rewrite from scratch, rather than attempting to
piece together the workings of an often poorly documented system written
with "ancient" methods/languages.

</div>

<div>



</div>

<div>

Hence, onto the first item on the Joel Test: source control.

</div>

<div>



</div>

<div>

But not just any source control. [GitHub](https://github.com/).

</div>

<div>



</div>

<div>

Why GitHub? Well, first, it has the elusive "Alpha Coder mindshare".
While it may not matter one way or another to your business that the
Linux kernel, Git itself, jQuery, Ruby on Rails, and a host of other
important projects exist on GitHub, it matters to your programmers,
whether they know it or not (and the good ones will know it).

</div>

<div>



</div>

<div>

All of these actively maintained open source projects provide something
more interesting than mindshare: examples. Pick a programming language,
and you will very likely find an interesting project or two on GitHub
that has something worth learning. It may even prove to be the Rosetta
stone of programming languages -- you may find solutions to the same
problem in many different programming languages.

</div>

<div>



</div>

<div>

Second, [Social
Coding](http://radar.oreilly.com/2009/01/github-making-code-more-social.html).
Everyone knows of the usefulness of social networks -- they existed
before, but it's the tools that made them marketable/actionable. Social
coding in GitHub takes the usual forms -- followers, blogs, wikis,
issues, teams, organizations -- plus some more useful ones (e.g. the
[GitHub API](http://develop.github.com/)).

</div>

<div>



</div>

<div>

We used Team Foundation Server. It was a nice tool in our .NET
development shop -- a bit painful to setup with it's dependence on
SharePoint, but useful. However, it didn't scale too well in terms of
collaborators. We needed to add them as users into Active Directory,
fuss about with SharePoint and licensing, and so forth.

</div>

<div>



</div>

<div>

So next we tried [CodePlex](http://www.codeplex.com/). CodePlex was,
essentially, TFS in the cloud, and it mostly worked. There were capacity
issues, and it wasn't always friendly with non .NET languages, but the
main reason we didn't adopt it wholesale was:

</div>

<div>

1.  No way to make private repositories
2.  Often painful to connect into
3.  Went down/was slow often enough that we didn't want to rely on it.

<div>

This really illustrates the third virtue of GitHub, that it's a true
cloud service -- but cloud computing is all the hype right now and I
really wanted to illustrate it's particular benefits in this instance.

</div>

</div>

<div>



</div>

<div>

In going with GitHub, we created an organization for our, well,
organization. This gives us several important advantages over CodePlex:

</div>

<div>

1.  Private repositories
2.  Teams
3.  Unlimited collaborators (in particular, we can mix and match between
    general GitHub accounts and team members)
4.  Blogs, Wikis, Gists, Issue Trackers with voting, per-line file
    commenting, and other social features
5.  Works well with any programming language
6.  Fast, decentralized development (Git works locally, so you can get
    on a plane, code, and upload your changes once you've got internet
    access)
7.  Reliable versioning (Git uses hashes for files)
8.  Works well with any OS/IDE (Git has integration with Visual Studio,
    Eclipse, XCode plus command-line versions in most every OS)
9.  Git is a well-regarded distributed version control system (DCVS)

<div>

My programming team ported projects over from TFS and CodePlex in under
a day. By following projects, I can watch check-ins, view version
differences, open/close issues, and do all the usual software management
stuff without getting in the way. (Or better yet, delegate.)

</div>

</div>

<div>



</div>

<div>

The fees are pretty nominal (organizations get charged based on the
numbers of private repositories they want; public ones are free). GitHub
is hosted by RackSpace, so the reliability has been better than our
in-house TFS boxes. Today I just added someone outside our organization
to one of our projects with minimal hassle.

</div>

<div>



</div>

<div>

If you're going to be digging up fossilized code, Git and GitHub are
fairly pleasant tools for the job.

</div>

<div>



</div>

<div>

Look at the time! This isn't really everything I wanted to say, but I've
probably said enough for now (and I have other pressing priorities
including my own research), so I'll leave further pontificating for
another time.

</div>

<div>



</div>

<div>

I hope this was informative, or at least, entertaining!

</div>

<div>



</div>

<div>

(You can find me on GitHub [here](https://github.com/acgetchell)!)

</div>

<div>



</div>

</p>
