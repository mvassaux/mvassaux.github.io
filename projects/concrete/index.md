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

Here is a short description of the research carried during my [Ph.D.](https://hal.archives-ouvertes.fr/tel-01140988){: target="_blank"} at the [Laboratoire de Mécanique et Technologie](http://lmt.ens-paris-saclay.fr/){: target="_blank"} de l'ENS Paris-Saclay (formerly ENS Cachan).

<!-- **figure: modelling methodology (add links to seism, deap, concyc, cast3m)** -->

## science
{: name="science"}

<!-- <a name="science"></a> -->

Accurate simulation of massive reinforced concrete structures facing cyclic loading such as containment walls in nuclear power plants during a earthquake, requires precise and stable constitutive models that can be used jointly with finite element models. One of their key features is their ability to reproduce the amount of dissipated energy partly due to fracture and partly due to mechanisms associated to oscillatory loadings.

<img src="/static/soutenance.001.jpeg" class="full-width">
**highway to the prediction of the stability**: methodology to predict from rare experimental data the stability of high-risk reinforced concrete structures such as containment buildings in nuclear power-plants facing earthquakes.

---

The research focused on studying and modelling concrete at two-scales: the scale of a batch of concrete and the scale of an engineering structural element. I tried to understand and model the mechanical behaviour of concrete under cyclic loading, which is inherently complicated by the closure of cracks, causing gradual regain of stiffness, but most unexpectedly hysteresis.

<!-- **figure: a cracked wall** -->
<!-- **figure: uniaxial behaviour vs. zoom on closing crack** -->

Using a microscopic scale model for concrete, assuming homogeneity of the constituents but explicit description of cracking and partial representativity of cracks roughness, we have explored mechanisms related to cyclic loadings. Monitoring contact and friction in formed cracks in a few centimetres large piece of concrete, we have been able to understand how internal self-balanced pre-strains, released at cracking, can generate gradual stiffness recovery and hysteresis during unloading [[1]](#pregul).


<img src="/static/cw38_amp10_web.gif" class="full-width">

**a not-so-simple shear test**: simulation of a cracked concrete sample facing shear, showing strong crack surfaces interaction.

---

<!-- Well, that is set aside now, scale effects in fracture still have to be figured out. -->

## developments
{: name="devs"}

On the development side of things, which was most of my PhD allocation, I spent my time developing the microscale model of a batch of concrete. Originally it was an existing lattice model that I extended to a particle-based model, or as we call it now a beam-particle model [[2]](#pbeam). In short, the continuum is discretised using Voronoï tessellation, polygonal particles are initially linked by brittle beams, and upon their failure can interact further by contact and friction. To enhance numerical stability, which was severely impaired by the simultaneous integration of brittle failure, contact and friction, I also redesigned the solution algorithm to solve quasi-static equilibrium [[3]](#plattice).
<!-- The whole code is freely available on github **ref: github/deap** . -->

Findings on the microscale mechanisms related to cracks closure led us to the formulation of a constitutive model for quasi-brittle materials cyclically loaded with enhanced numerical stability [[1]](#pregul). The model ([source](http://www-cast3m.cea.fr/index.php?page=sources&source=concyc2){: target="_blank"}, [example](http://www-cast3m.cea.fr/index.php?page=exemples&exemple=concyc){: target="_blank"}, [notice](http://www-cast3m.cea.fr/index.php?page=notices&notice=MODE#ENDOMMAGEMENT){: target="_blank"}) is now implemented and available in the open-source structural analysis and fluid mechanics software [Cast3M](http://www-cast3m.cea.fr/){: target="_blank"} based on the finite element method developed at the CEA.

## publications
{: name="publications"}

[1] Maxime Vassaux, Benjamin Richard, Frédéric Ragueneau, and Alain Millard.<br>[*Regularised crack behaviour effects on continuum modelling of quasi-brittle materials under cyclic loading.*](https://hal.archives-ouvertes.fr/hal-01271756/){: target="_blank"}<br>Engineering Fracture Mechanics, 149 (2015): 18-36.
{: id="pregul"}

[2] Maxime Vassaux, Cécile Oliver-Leblond, Benjamin Richard, and Frédéric Ragueneau.<br>[*Beam-particle approach to model cracking and energy dissipation in concrete: Identification strategy and validation.*](http://hal.upmc.fr/hal-01297333){: target="_blank"}<br>Cement and Concrete Composites, 70 (2016): 1-14.
{: id="pbeam"}

[3] Maxime Vassaux, Benjamin Richard, Frédéric Ragueneau, Alain Millard, and Arnaud Delaplace.<br>[*Lattice models applied to cyclic behavior description of quasi‐brittle materials: advantages of implicit integration.*](https://hal.archives-ouvertes.fr/hal-01177051){: target="_blank"}<br>International Journal for Numerical and Analytical Methods in Geomechanics, 39 (2015): 775-798.
{: id="plattice"}
