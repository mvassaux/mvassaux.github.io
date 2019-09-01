---
layout: post
title: stability of concrete structures under seismic loading
skip_related: true
---

<!--
* decompose in three pages, accessed in header unfolding menu under projects

* or pop each of these pages from the figure on the main page

* contour separately science and devs parts on each topic

* recap links at bottom
-->

<!-- Let's go to the [science](#science) bit or the [devs](#devs) one... -->

I completed my [Ph.D.](https://hal.archives-ouvertes.fr/tel-01140988){: target="_blank"} thesis at the [Laboratoire de Mécanique et Technologie](http://lmt.ens-paris-saclay.fr/){: target="_blank"} de l'ENS Paris-Saclay (formerly ENS Cachan), from 2012 to 2015, largely helped by the support of our horrendously big group of PhD students, and the always running coffee machine.

<!-- **figure: modelling methodology (add links to seism, deap, concyc, cast3m)** -->

## the science
{: name="science"}

<!-- <a name="science"></a> -->

Safety first! Thus, the structural integrity of nuclear power plants is deemed important. From that interesting observation, knowing in advance how containment walls in nuclear power plants react to an earthquake popping up nearby is essential. With a hint of abstraction, this problem can be rephrased as trying to develop accurate simulations of massive reinforced concrete structures facing cyclic loading paths. One of the key piece of information these simulations need to provide is *how* cracks form in concrete structures, and more precisely *how much*. Indeed, leaks in nuclear power plants containment walls are rarely a good thing...

The standard method to model such large structures is to consider the whole as a continuum, and therefore apply continuum mechanics. Equilibrium equations are solved using the finite element method, and the behaviour of the material is described using as precise and stable constitutive equations as possible. A key feature of these constitutive equations is their ability to reproduce the amount of dissipated energy partly due to fracture and partly due to mechanisms associated to oscillatory loadings.

<img src="/static/soutenance.001.jpeg" class="full-width">
**highway to the prediction of the stability**: methodology to predict from rare experimental data the stability of high-risk reinforced concrete structures such as containment buildings in nuclear power-plants facing earthquakes.

---

My research focused on studying and modelling concrete at two-scales: the scale of a batch of concrete and the scale of an engineering structural element. I tried to understand and model the mechanical behaviour of concrete under cyclic loading. Closure of cracks during unloading and reverse loading, causes a gradual regain of stiffness, but more surprisingly hysteresis.

<!-- **figure: a cracked wall** -->
<!-- **figure: uniaxial behaviour vs. zoom on closing crack** -->

Using a microscopic scale model for concrete, assuming homogeneity of the constituents but explicit description of cracking and partial representativity of cracks roughness, we explored failure under compressive loading [[1]](#pcomp) and later, phenomena arising under cyclic loadings. Monitoring contact and friction in formed cracks in a few centimetres large piece of concrete, we were able to understand how internal self-balanced pre-strains, released at cracking, can generate gradual stiffness recovery and hysteresis during unloading [[2]](#pregul).


<img src="/static/cw38_amp10_web.gif" class="full-width">

**a not-so-simple shear test**: simulation of a cracked concrete sample facing shear, showing significant crack surfaces interaction.

---

<!-- Well, that is set aside now, scale effects in fracture still have to be figured out. -->

## the devs
{: name="devs"}

On the development side of things, which is what I did most during PhD project, I spent my time developing a microscale model of a batch of concrete. Originally it was an existing lattice model that I extended to a particle-based model, or as we call it now a beam-particle model [[3]](#pbeam). In short, the continuum is discretised using Voronoï tessellation, polygonal particles are initially linked by brittle beams, and upon their failure can interact further by contact and friction. To enhance numerical stability, which was severely impaired by the simultaneous integration of brittle failure, contact and friction, I also redesigned the solution algorithm to solve quasi-static equilibrium [[4]](#plattice).
<!-- The whole code is freely available on github **ref: github/deap** . -->

Findings on the microscale mechanisms related to cracks closure led us to the formulation of a constitutive model for quasi-brittle materials cyclically loaded with enhanced numerical stability [[2]](#pregul). The model ([source](http://www-cast3m.cea.fr/index.php?page=sources&source=concyc2){: target="_blank"}, [example](http://www-cast3m.cea.fr/index.php?page=exemples&exemple=concyc){: target="_blank"}, [notice](http://www-cast3m.cea.fr/index.php?page=notices&notice=MODE#ENDOMMAGEMENT){: target="_blank"}) is now implemented and available in the open-source structural analysis and fluid mechanics software [Cast3M](http://www-cast3m.cea.fr/){: target="_blank"} based on the finite element method developed at the CEA.

## the publications
{: name="publications"}

[1] Maxime Vassaux, Benjamin Richard, Frédéric Ragueneau, and Alain Millard.<br>[*Compressive behavior of a lattice discrete element model for quasi-brittle materials.*](https://books.google.fr/books?hl=en&lr=&id=0ILMBQAAQBAJ&oi=fnd&pg=PA335&dq=info:EweH1g5_0R4J:scholar.google.com&ots=skSm6VjufF&sig=_Ez0S7tRGUYrDu2sfogG4Dn-9sw&redir_esc=y#v=onepage&q&f=false){: target="_blank"}<br>Computational Modelling of Concrete Structures, 1 (2014): 335-344.
{: id="pcomp"}

[2] Maxime Vassaux, Benjamin Richard, Frédéric Ragueneau, and Alain Millard.<br>[*Regularised crack behaviour effects on continuum modelling of quasi-brittle materials under cyclic loading.*](https://hal.archives-ouvertes.fr/hal-01271756/){: target="_blank"}<br>Engineering Fracture Mechanics, 149 (2015): 18-36.
{: id="pregul"}

[3] Maxime Vassaux, Cécile Oliver-Leblond, Benjamin Richard, and Frédéric Ragueneau.<br>[*Beam-particle approach to model cracking and energy dissipation in concrete: Identification strategy and validation.*](http://hal.upmc.fr/hal-01297333){: target="_blank"}<br>Cement and Concrete Composites, 70 (2016): 1-14.
{: id="pbeam"}

[4] Maxime Vassaux, Benjamin Richard, Frédéric Ragueneau, Alain Millard, and Arnaud Delaplace.<br>[*Lattice models applied to cyclic behavior description of quasi‐brittle materials: advantages of implicit integration.*](https://hal.archives-ouvertes.fr/hal-01177051){: target="_blank"}<br>International Journal for Numerical and Analytical Methods in Geomechanics, 39 (2015): 775-798.
{: id="plattice"}
