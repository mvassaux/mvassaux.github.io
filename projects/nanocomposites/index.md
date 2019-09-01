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

Polymer and derived nanocomposites are hierarchically structured materials. They display a unique architecture at each scale they are looked at. With an engineering application in mind, each of these architectures can be modified, choosing a specific polymer, or adding tailor-made particles, in order to tweak the physical properties of the resulting material.

<img src="/static/hmm_bicomposite_lo.jpg">

**complex on so many levels**: stress localisation in a continuum piece of graphene epoxy composite; the continuum scale model probes on two types of atomic systems involving single or double graphene reinforcement; the two types of composites are arranged in a diagonal pattern in the continuum.

---

We model and couple the different scales using the relevant computational techniques, thus we are able to investigate in detail how the addition of nanoparticles impact the behaviour of polymer nanocomposites. While applying loading conditions representative of the engineering continuum scale, we can observe of the different constituents of the material interact at the chemical atomic scale. In turn, we are able to tune and optimise the atomic structure of the material to improve macroscopic properties, such as the fracture toughness.

<div>
  <div style="float: left; width: 30%">
    <img src="/static/g1_distribution_shell_web.png">
  </div>
  <div style="float: right; width: 30%">
    <img src="/static/g0_nrep1_impact_25fps.gif">
  </div>
  <div style="float: right; width: 30%">
    <img src="/static/dropweight_atomistic.gif">
  </div>
</div>

**let's give it a shot**: simulation of a high-velocity impact on a composite shell made of pure epoxy cells and graphene-epoxy nanocomposite cells (left); the impact produces propagating compression and shear waves in the shell (middle); the atomic structure of the nanocomposite located found at the centre of the shell faces high-frequency oscillations of mixed strains.
---

We mainly focus on fracture properties of polymer nanocomposites. We study how properties such as elastic modulus, strength and toughness are impacted, by structural heterogeneities at different scales. Currently, we apply our method to the interaction between the polymer cross-linked structure of epoxy at the nanoscale and sheets of graphene that expand up to the microscale and the macroscale. More specifically, we have been able to explore how seemingly ductile materials at the nanoscale such as epoxy resins, become brittle at the macroscale.

## the devs
{: name="devs"}

Exploring the interaction between mechanisms at different scales, requires either a fine scale model extended up to the coarser scales (in space and time) and an extremely high amount of computational power, or a wise separation of scales in multiple models and still a huge amount of computational power, but reduced enough so that these models can be simulated on the world's biggest supercomputers.

At the moment, I develop a coupling library, simplistically called [DeaLAMMPS](https://github.com/mvassaux/DeaLAMMPS/){: target="_blank"} based on the Heterogeneous Mutliscale Method, that allows to simulate a atomic and a continuum model concurrently [[1]](#phmm). As such, the two models can exchange mechanical information and therefore we are able to understand how the interplay between the two scales. The coupling is achieved by transfer of homogenised strains and stresses.

<!-- <img src="../../static/dogbone.gif" width="400"> -->
<!-- **video: macroscale dogbone test and nanoscale tensile test** -->

At the nanoscale we have developed an all-atom model of epoxy resin and epoxy resin traversed by a graphene sheet using [LAMMPS](http://lammps.sandia.gov/){: target="_blank"}, a molecular dynamics package. And, at the microscale we have developed continuum two-phase model, which derives stresses at a given strain based on nanoscale simulations. Continuum mechanics equations are solved using [Deal.II](https://www.dealii.org/){: target="_blank"}, a finite element method library.

An average two-scale simulation runs for a few hundreds of thousands of core hours. Thanks to allocations on supercomputers across Europe (ARCHER/UK, SuperMUC/Germany, PROMETHEUS/Poland), such highly parallel workflows are completed in a couple of days. This work is part of the European project [ComPat](http://www.compat-project.eu/), which aims at identifying patterns in computational workflows and automate the optimisation of their execution on several, distant resources. We took part in the optimisation of computational patterns, where a "master" algorithm relies on operations performed by several instantiations of a "slave" algorithm, launched dynamically. The efficiency of such distributed workflow is guaranteed using a Pilot Job Manager, that executes asynchronously the many instances of the "slave" algorithm, LAMMPS. The scheduling of these independent simulations across several the aforementioned HPC platforms is performed considering the queueing time, the execution time and the energy efficiency of the different platforms.

In attempt to switch from physic-based to data-based modelling, we use gaussian processes, in a first time, to replace partly the execution of the "slave" algorithm. After a certain number of executions the output (stress) of the algorithm given a certain input (strain) can be interpolated simply on prior results. Indeed, reducing drastically the computational costs. This data-driven modelling technique is performed using the [scikit-learn](http://scikit-learn.org) machine learning library. Most of the complexity is induced by the application of such regression technique to highly non-linear physics (fracture), where the features and their similarity are non-obvious.

## the publications
{: name="publications"}

[1] Maxime Vassaux, Robin A. Richardson and Peter V. Coveney.<br>[*The heterogeneous multiscale method applied to inelastic polymer mechanics.*](https://doi.org/10.1098/rsta.2018.0150){: target="_blank"}<br>Philosophical Transactions of the Royal Society A, 377, 2142 (2019).
{: id="phmm"}

[2] Maxime Vassaux, Robert C. Sinclair, Robin A. Richardson, James L. Suter and Peter V. Coveney.<br>[*The role of graphene in enhancing the material properties of thermosetting polymers.*](https://doi.org/10.1002/adts.201800168){: target="_blank"}<br>Advanced Theory and Simulations, 2, 5 (2019).
{: id="pgrap"}

[3] Maxime Vassaux, Robert C. Sinclair, Robin A. Richardson, James L. Suter and Peter V. Coveney.<br>[*Toward high fidelity materials property prediction from multiscale modeling and simulation.*](https://doi.org/10.1002/adts.201800168){: target="_blank"}<br>Advanced Theory and Simulations, In press (2019).
{: id="ptowa"}
