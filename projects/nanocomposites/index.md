---
layout: post
title: hierarchical toughening of polymer nanocomposites
skip_related: true
---

<!--
* decompose in three pages, accessed in header unfolding menu under projects

* or pop each of these pages from the figure on the main page

* contour separately science and devs parts on each topic

* recap links at bottom
-->

Shortly before my funding was running out in Marseille, I started to have a decent idea of what I wanted like to explore on the long-run: relations between the cell mechanical environment and epigenetics. That is a very long shot, especially using computational models. Nevertheless, mentioning this at a few conferences, nobody said it was *entirely* stupid, so I started to believe... maybe... However, I was far from mastering the techniques to model anything below the scale of the cell nucleus. Long story short, got lucky, I found a position in London at the [Centre for Computational Science](http://ccs.chem.ucl.ac.uk/){: target="_blank"} at University College London, where I had to develop a tool to couple a method I knew, the Finite Element Method, and a method I needed to learn to model atomic systems, All-Atom Molecular Dynamics, being useful and learning at the same time!

## the science
{: name="science"}

What if we could predict the material properties (Young modulus, thermal conductivity, and so on...) of a chemical compound for its atomic structure? To predict these properties computationally, we would need to simulate volumes of material of the order of the cubic centimetre, at the smallest, with details of the order of the nanometre, at the largest. Hopefully, there are a few simplifications we can perform, all the structural details from one end to the other need not to be considered, all the time, everywhere.

Polymer and derived nanocomposites are hierarchically structured materials, their structure evolves across the scales. Certain, characteristic scales, influence most significantly the behaviour of the nanocomposite. The structure of the material at these characteristic scales need to be considered in our models. At other scales, the information can, at first, be neglected. In short that is the philosophy of the methods developed at the Centre for Computational Science even before the start of this project [[1]](#ptowa).

Once we understand how the structure at each of these scales control the physics of the material, these structures can also be customised. Choosing a specific polymer, or adding tailor-made particles, for example, the properties of the resulting material can be enhanced with an engineering application in mind.

We modelled and coupled two characteristic scales: (i) the atomic structure using molecular dynamics, and (ii) the testing structure using the finite element method [[2]](#phmm). We were able to investigate how the addition of 2d-nanoparticles impact the response of thermosetting polymer to standard engineering tests, such as the dogbone tension test, the compact tension test or the drop-weight impact test. While applying loading conditions representative of the engineering continuum scale, our models enable to observe how the different constituents of the material interact at the atomic scale.

<div>
  <div style="float: left; width: 50%; padding-bottom: 40px">
    <img src="/static/g1_distribution_shell_web.png">
  </div>
  <div style="float: left; width: 50%; padding-top: 40px">
    <img src="/static/g0_nrep1_impact_25fps.gif">
  </div>
</div>  

<div>
  <div style="float: right; width: 60%; padding-left: 120px; padding-right: 30px">
    <img src="/static/dropweight_atomistic.gif">
  </div>
</div>

**let's give it a shot**: simulation of a high-velocity impact on a composite shell made of pure epoxy cells and graphene-epoxy nanocomposite cells (top, left); the impact produces propagating compression and shear waves in the shell (top, right); the atomic structure of the nanocomposite located found at the centre of the shell faces high-frequency oscillations of mixed strains (bottom).

---

We mainly focused on fracture properties of the nanocomposites as it is a critical parameter in aeronautical design. We applied our multiscale modelling method to study how the material's strength and toughness can be impacted by 2d-nanoparticles characteristics, for example their size, their thickness or their volume ratio. In the mean time we explored how thermosetting polymers such as epoxy resins, seemingly ductile at the nanoscale can become brittle at the macroscale. Quite unexpectedly, we first came to conclude that adding graphene nanoparticles in epoxy resins reduces drastically dissipated energy via internal friction during an impact test (see figure above). In other words, the nanoparticles enhance the elastic behaviour, energy restitution, of the thermosetting polymer [[3]](#pgrap). These conclusions might not be extremely useful for airplane design, as impact rather need to be absorbed... but plenty of applications in sports performance, synthetic tissue engineering or energy-saving prosthetics could definitely benefit from these!

## the devs
{: name="devs"}

Methods and softwares available to simulate atomic and continuum systems are already plenty. At the nanoscale we developed an all-atom model of epoxy resin and epoxy resin traversed by a graphene sheet using [LAMMPS](http://lammps.sandia.gov/){: target="_blank"}, a molecular dynamics package. And, at the microscale we developed continuum two-phase model which equations were solved using [Deal.II](https://www.dealii.org/){: target="_blank"}, a finite element method library. I initiated the development a coupling library, which name I didn't think to much about, called [DeaLAMMPS](https://github.com/mvassaux/DeaLAMMPS/){: target="_blank"}. The resulting software based on the heterogeneous mutliscale method allows to simulate a atomic and a continuum model concurrently [[2]](#phmm). The coupling is achieved by transfer of homogenised strains from the continuum to the atomic system and stresses the other way around. The two models exchanging mechanical information are, in result, loosely coupled and made it possible to understand how the interplay between the two given scales.

<img src="/static/hmm_bicomposite_lo.jpg">

**complex on so many levels**: stress localisation in a continuum piece of graphene epoxy composite; the continuum scale model probes on two types of atomic systems involving single or double graphene reinforcement; the two types of composites are arranged in a diagonal pattern in the continuum.

---

An average two-scale simulation runs requires a few hundreds of thousands of core hours, simply put, quite a lot of computational energy... Thanks to allocations on supercomputers across Europe (ARCHER/UK, SuperMUC/Germany, PROMETHEUS/Poland), and a lot of optimisation in CPU usage, such highly parallel simulations were completed in a couple of days. Optimising multiscale parallel workflows was part of the European project [ComPat](http://www.compat-project.eu/). The project aimed at identifying patterns in computational workflows and automate the optimisation of their execution on several, distant resources, such as supercomputers. We took part in the optimisation of the execution of the computational patterns, where a "master" algorithm relies on operations performed by several instantiations of a "slave" algorithm, launched dynamically, asynchronously.
<!-- The efficiency of such distributed workflow is guaranteed using a Pilot Job Manager, that executes asynchronously the many instances of the "slave" algorithm, LAMMPS. The scheduling of these independent simulations across several the aforementioned HPC platforms is performed considering the queueing time, the execution time and the energy efficiency of the different platforms. -->

Running loads of multiscale simulations, coordinating large amounts of computations, might already be an achievement, however it is not considered sufficient to simply predict a result, that is property or mechanism. For any prediction to be trusted and worth acting upon, we better have an idea of its accuracy. Similarly to what experimentalists do, at least what I hope they do, tests need to be repeated to quantify confidence in the results. Uncertainty in simulations arises from many sources that can be grouped in three types: input parameter errors, verification errors (computer precision, mathematical accuracy), validation error (physical accuracy, range of validity). Quantifying uncertainty of multiscale simulations is the purpose of the European project [VECMA](http://www.vecma.eu/), which led to the development of the VECMA toolkit [[4]](#pvecm). The toolkit provides a suite of algorithms drawing from the specific structure of multiscale workflows to avoid the unbearable cost of Monte-Carlo methods to quantify uncertainty.

<!-- In attempt to switch from physic-based to data-based modelling, we use gaussian processes, in a first time, to replace partly the execution of the "slave" algorithm. After a certain number of executions the output (stress) of the algorithm given a certain input (strain) can be interpolated simply on prior results. Indeed, reducing drastically the computational costs. This data-driven modelling technique is performed using the [scikit-learn](http://scikit-learn.org) machine learning library. Most of the complexity is induced by the application of such regression technique to highly non-linear physics (fracture), where the features and their similarity are non-obvious. -->



## the publications
{: name="publications"}

[1] Maxime Vassaux, Robert C. Sinclair, Robin A. Richardson, James L. Suter and Peter V. Coveney.<br>[*Toward high fidelity materials property prediction from multiscale modeling and simulation.*](https://doi.org/10.1002/adts.201900122){: target="_blank"}<br>Advanced Theory and Simulations, In press (2019).
{: id="ptowa"}

[2] Maxime Vassaux, Robin A. Richardson and Peter V. Coveney.<br>[*The heterogeneous multiscale method applied to inelastic polymer mechanics.*](https://doi.org/10.1098/rsta.2018.0150){: target="_blank"}<br>Philosophical Transactions of the Royal Society A, 377, 2142 (2019).
{: id="phmm"}

[3] Maxime Vassaux, Robert C. Sinclair, Robin A. Richardson, James L. Suter and Peter V. Coveney.<br>[*The role of graphene in enhancing the material properties of thermosetting polymers.*](https://doi.org/10.1002/adts.201800168){: target="_blank"}<br>Advanced Theory and Simulations, 2, 5 (2019).
{: id="pgrap"}

[4] Derek Groen, Robin A. Richardson, David W. Wright, Vytautas Jancauskas, Robert C. Sinclair, Paul Karlshoefer, Maxime Vassaux, Hamid Arabnejad, Tomasz Piontek, Piotr Kopta, Bartosz Bosak, Jalal Lakhlili, Olivier Hoenen, Diana Suleimenova, Wouter Edeling, Daan Crommelin, Anna Nikishova and Peter V. Coveney.<br>[*Introducing VECMAtk – verification, validation and uncertainty quantification for multiscale and HPC simulations.*](https://doi.org/10.1007/978-3-030-22747-0_36){: target="_blank"}<br>In: Rodrigues J. et al. (eds) Computational Science – ICCS. Lecture Notes in Computer Science, vol 11539. Springer, Cham (2019).
{: id="pvecm"}
