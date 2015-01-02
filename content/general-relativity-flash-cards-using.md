Title: General Relativity flash-cards using Anki
Date: 2013-10-24 05:52
Author: Adam Getchell
Tags: general relativity
Category: Physics
Slug: general-relativity-flash-cards-using

[Anki](http://ankisrs.net/) is a neat [spaced repetition
system](http://www.supermemo.com/english/ol/background.htm) that allows
you to maximize memorization efficiency, or something like that.
Interestingly, I came across it on the [Clojure
group](http://groups.google.com/group/clojure), and there are already
[decks available for learning
Clojure](http://blog.milehighcode.com/2012/01/use-you-spaced-repetition-system-for.html).
It accepts LaTeX, so I've decided to make a flash-deck of some handy
formulas that pop up in General Relativity, because there's enough to
learn without forgetting!  

(Also, it's handy to have LaTeX snippets someplace semi-permanent.)  

Bianchi identity:  

$$\nabla_{[\lambda}R_{\rho\sigma]\mu\nu}=0$$  

Christoffel symbol:  

$$\Gamma_{\mu\nu}^{\lambda}=\frac{1}{2}g^{\lambda\sigma}\left(\partial_{\mu}g_{\nu\sigma}+\partial_{\nu}g_{\sigma\mu}-\partial_{\sigma}g_{\mu\nu}\right)$$  

Covariant derivative of a 1-form:  

$$\nabla_{\mu}\omega_{\nu}=\partial_{\mu}\omega_{\nu}-\Gamma_{\mu\nu}^{\lambda}\omega_{\lambda}$$  

Covariant derivative of a vector:  

$$\nabla_{\mu}V^{\nu}=\partial_{\mu}V^{\nu}+\Gamma_{\mu\lambda}^{\nu}V^{\lambda}$$  

Covariant form of Maxwell's equations:

$$\partial_{\mu}F^{\nu\mu}=J^{\nu}$$  

$$\partial_{[\mu}F_{\nu\lambda]}=0$$  

for  

$$J^{\nu}=\left(\rho,J^{x},J^{y},J^{z}\right)$$  

and  

$$F_{\mu\nu}=\left(
\begin{array}{cccc}  
0 & -E_{1} & -E_{2} & -E_{3} \\  
E_{1} & 0 & B_{3} & -B_{2} \\  
E_{2} & -B_{3} & 0 & B_{1} \\  
E_{3} & B_{2} & -B_{1} & 0  \\
\end{array}
\right)$$

Riemann tensor:  

$$R_{\sigma\mu\nu}^{\rho}=\partial_{\mu}\Gamma_{\nu\sigma}^{\rho}-\partial_{\nu}\Gamma_{\mu\sigma}^{\rho}+\Gamma_{\mu\lambda}^{\rho}\Gamma_{\nu\sigma}^{\lambda}-\Gamma_{\nu\lambda}^{\rho}\Gamma_{\mu\sigma}^{\lambda}$$  

Properties of the Riemann tensor:  


$$R_{\rho\sigma\mu\nu}=-R_{\sigma\rho\mu\nu}$$  

$$R_{\rho\sigma\mu\nu}=-R_{\sigma\rho\nu\mu}$$  

$$R_{\rho\sigma\mu\nu}=R_{\mu\nu\rho\sigma}$$  

$$R_{\rho[\sigma\mu\nu]}=0$$  


Ricci tensor:  

$$R_{\mu\nu}=R_{\mu\lambda\nu}^{\lambda}$$  

Ricci scalar:  

$$R=R_{\mu}^{\mu}=g^{\mu\nu}R_{\mu\nu}$$  

Einstein tensor:  

$$G_{\mu\nu}=R_{\mu\nu}-\frac{1}{2}Rg_{\mu\nu}$$  

Formulae from Sean Carroll's *[Spacetime and Geometry: An Introduction
to General
Relativity](http://preposterousuniverse.com/spacetimeandgeometry/)*  

Anki synchronizes with DropBox, but it's [a bit
involved](http://ankisrs.net/docs/SyncingMedia.html). When I get my deck
synchronized and uploaded, I will post a link to it.  

Update: <https://ankiweb.net/shared/info/1777635479>
