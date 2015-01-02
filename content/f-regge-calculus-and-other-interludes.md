Title: F#, Regge Calculus, and other interludes
Date: 2007-11-19 05:39
Author: Adam Getchell
Tags: quantum gravity, .net, information theory, thermodynamics, quantum mechanics, f#
Slug: f-regge-calculus-and-other-interludes
Category: Physics

Still working on [Causal Dynamical
Triangulations](http://adamgetchell.blogspot.com/2007_10_01_archive.html),
I've also taken some time out to (start to) learn a delightful new
functional programming language,
[F\#](http://research.microsoft.com/fsharp/fsharp.aspx), with the help
of a good [site](http://cs.hubfs.net/), online
[journal](http://www.ffconsultancy.com/products/fsharp_journal/), and
this [book](http://strangelights.com/). Mixing functional, imperative,
and object-oriented programming with good mathematics features and the
.NET framework allows me to blend work and academics. The goal is to
write a first-cut CDT program in F\# and refine as necessary ....  

CDTs depend upon [Regge
calculus](http://en.wikipedia.org/wiki/Regge_calculus), which is
essentially a prescribed way for dividing up spacetime into a discrete
lattice (simplexes) while adhering to the Einstein field equations.
(Regge calculus is explained in detail in Chapter 41 of [Gravitation,
aka the Big Black
Book](http://www.amazon.com/Gravitation-Physics-Kip-S-Thorne/dp/0716703440/ref=ed_oe_p/002-3874810-3091246).)  

In particular, you divide up a smooth 4-manifold into a collection of
4-d simplexes, in the same way you can divide up a 3-sphere into the
(2-)triangles of the icosohedron. If you pressed the icosohedron
perfectly flat onto a plane, you would see <span
style="font-style: italic;">deficit angles</span> or <span
style="font-style: italic;">hinges</span> that essentially reflect the
its spherical curvature. In the same way, you analyze the simplices of
the 4-d manifold to determine its curvature.  

If you are extraordinarily careful in how you setup your lattice, you
can perfectly constrain your volume using just fixed edge lengths. (For
example, a [tiling](http://en.wikipedia.org/wiki/Tessellation) of
triangles constrains a surface rigidly, because the tiling cannot be
deformed without changing edge lengths. A tiling of squares does not,
because the squares can be squashed sideways into parallelograms without
changing their edge lengths.)  

And if you do this, you can now examine that volume (or brane, or bulk )
by solving the Einstein equations expressed in terms of conditions on
the hinge angles (which are themselves functions only of the edge
lengths). This is exciting because you can now program a computer
(carefully) to solve problems that don't lend themselves to analytic
solution, which allows you to do interesting things:  

[Discrete quantum gravity in the framework of Regge calculus
formalism](http://arxiv.org/PS_cache/gr-qc/pdf/0506/0506071v2.pdf)  

In the past few weeks, I've also taken time to read up on a few areas of
interest.  

Perhaps one of the more interesting recent occurrences is the recent
re-examination of the 2nd law of thermodynamics, long thought to be
inviolable and one of the most solid foundations of physics by such
luminaries as Maxwell, Einstein, Eddington, and Brilloun.  

Physics is always fun, check your assumptions at the door!  

First, a nice publicly accessible summary:  

[Why Do We Believe in the Second
Law?](http://arxiv.org/PS_cache/cond-mat/pdf/0208/0208291v1.pdf), T.
Duncan  

The <span style="font-style: italic;">Foundations of Physics</span>
journal, Volume 37, Number 12/December 2007 is devoted to this
extraordinary topic (unfortunately, e-journal subscriptions required to
view), starting with Geraard t'Hooft's
[editorial](http://springerlink.metapress.com/content/4275497r4v43823p/fulltext.pdf),
which gives a broad summary of the scope of the papers in the journal.  

Next, we have:  
[  
The Second Law of Thermodynamics: Foundations and
Status](http://springerlink.metapress.com/content/lhj15642v3445722/fulltext.pdf),
by D.P. Sheehan  

This paper gives a broad overview on three classes of discussion
regarding the Second Law now underway: ideal gases, quantum
perspectives, and interpretations.  

[Information Loss as a Foundational Principle for the Second Law of
Thermodynamics](http://springerlink.metapress.com/content/c505876828551152/fulltext.pdf),
by T.L. Duncan and J.S. Semura  

This paper explores in detail the concept of information loss as being
the fundamental explanation for entropy, essentially casting the 2nd law
from "Entropy always increases for irreversible processes" to
"Information is always lost for irreversible processes". The authors
further argue that all classical derivations of the 2nd law using
"entropy" actually incorporate, explicitly or implicitly, information
loss as the mechanism.  

As an example, [Maxwell's
demon](http://en.wikipedia.org/wiki/Maxwell%27s_demon) is shown to be
able to violate the 2nd law on the basis of having information -- in
particular, knowing how to sort fast-moving from slow-moving particles.
However, creation of that information eventually involves the deletion
of a bit of information from storage -- for a subsequent Kln2 energy
cost -- which is argued as being the source of entropy. (All faults are
mine, not the authors, if I've paraphrased these arguments
incorrectly.)  

Jean E. Burns, in [Vacuum Radiation, Entropy, and Molecular
Chaos](http://springerlink.metapress.com/content/67143288r1652w14/fulltext.pdf),
makes a very interesting extension to classical entropy models for
isolated systems. Classical thermodynamic models separate the system
from the environment. The canonical example is the refrigerator, which
decreases temperature (thus entropy) locally, but at the expense of
expelling even more heat (thus increasing entropy) in the environment.
The entropy/heat loss inside the system is outweighed by the
entropy/heat gain in the environment.  

However, what happens for an arbitrarily large system (such as the
universe), where there is no external reservoir? Burns argues that
vacuum radiation provides the mechanism for entropy increase.  

Perhaps of most interest to biologists and science-fiction fans is
Sheehan's [Thermosynthetic
Life](http://springerlink.metapress.com/content/9km828746w91p011/fulltext.pdf),
which postulates the existence of life forms deriving their energy
solely from thermal energy. In addition to searches for extremophile
lifeforms (such as bacteria near volcanic vents) that fit this profile,
it provides an engaging test into the 2nd Law, because such life-forms
may well violate it!  

And, continuing on with our examinations into entropy and information
theory, we have:  

<span style="text-decoration: underline;"></span>[Information Recovery
from Black
Holes](http://www.worldscinet.com/ijmpd/mkt/preserved-docs/1512/S0218271806009765.pdf),
V. Balasubramanian, D. Marolf, and M. Rozali  

This first-place prizewinning essay of the 2006 Essay Competition of the
Gravity Research Foundation provides insights into two crucial
questions:  

1.  Why do classical black holes have finite entropy equal to a quarter
    of the horizon area?
2.  How does information escape from an evaporating black hole?

In essence (modulo a great many technical arguments), the answer to both
of these questions is that the finite mass black hole, representing a
finite number of energy states N, therefore possesses a discrete energy
spectrum. In general, discrete spectra are quantum-mechanically
non-degenerate, so knowledge of the precise energy and other (commuting)
conserved charges determines the quantum state. But General Relativity
charges are generically given by boundary terms; thus, the entire state
of the black hole resides in the boundary (asymptotic region), available
to all observers.  

This is at odds with classical GR, because there exist unobservable
regions within the black hole that are causally separated. However, in
the quantum mechanical case the Heisenberg Uncertainty principle
dictates that a "Heisenberg recurrence time" exists. This can be thought
of as a sort of spontaneous large thermal fluctuation in which the black
hole may be replaced by a ball of expanding hot gas. Although the gas
will re-collapse to form another black hole on a relatively short time
scale, during the span of its existence the full details of the black
hole's internal state are visible from infinity.  

And thus we see that at the quantum level, the event horizon becomes
ill-defined, and quantum mechanics, entropy, and information theory
collaborate against General Relativity to allow what was previously
thought to be impossible.  

And in a final bit of fun, we see a method for efficiently converting
black holes into gravitational waves:  
[  
Black Hole Bremsstrahlung: Can it be an efficient source of
gravitational
waves?](http://www.worldscinet.com/ijmpd/mkt/free/S0218271806009625.html)  

Taking a 2 solar mass black hole traveling at .38c and converting 90% of
its rest mass into a lobe-shaped pulse with width deltaU \~ 40 for 10E40
GeV\^2 sounds exciting!

</p>
