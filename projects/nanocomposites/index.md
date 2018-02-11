---
layout: post
title: Hierarchical toughening of polymer nanocomposites
skip_related: true
---

<!--
* decompose in three pages, accessed in header unfolding menu under projects

* or pop each of these pages from the figure on the main page

* contour separately science and devs parts on each topic

* recap links at bottom
-->

## science
{: name="science"}

Polymer and derived nanocomposites are hierarchically structured materials. Such materials display a various and specific architecture depending on the scale it is looked at. With an engineering application in mind, each of these architectures can be modified, choosing a specific polymer, or adding tailor-made particles, in order to tweak the physical properties of the resulting material.

We model and couple the different scales using the relevant computational techniques, thus we are able to investigate in detail how the addition of nanoparticles impact the behaviour of polymer nanocomposites. While applying loading conditions representative of the engineering continuum scale, we can observe of the different constituents of the material interact at the chemical atomic scale.

We mainly focus on fracture properties of polymer nanocomposites. We study how properties such as elastic modulus, strength and toughness are impacted, by structural heterogeneities at different scales. Currently, we apply our method to the interaction between the polymer cross-linked structure of epoxy at the nanoscale and sheets of graphene that expand up to the microscale.

## developments
{: name="devs"}

Exploring the interaction between mechanisms at different scales, requires either a fine scale model extended up to the coarser scales (in space and time) and an extremely high amount of computational power, or a wise separation of scales in multiple models and still a huge amount of computational power, but reduced enough so that these models can be simulated on the world's biggest supercomputers.

At the moment, I develop a coupling library, simplistically called [DeaLAMMPS](https://github.com/mvassaux/DeaLAMMPS/) based on the Heterogeneous Mutliscale Method, that allows to simulate a atomic and a continuum model concurrently. As such, the two models can exchange mechanical information and therefore we are able to understand how the interplay between the two scales. The coupling is achieved by transfer of homogenised strains and stresses.

<img src="../../static/dogbone.gif" width="400">
<!-- **video: macroscale dogbone test and nanoscale tensile test** -->

At the nanoscale we have developed an all-atom model of epoxy resin and epoxy resin traversed by a graphene sheet using [LAMMPS](http://lammps.sandia.gov/), a molecular dynamics package. And, at the microscale we have developed continuum two-phase model, which derives stresses at a given strain based on nanoscale simulations. Continuum mechanics equations are solved using [Deal.II](https://www.dealii.org/), a finite element method library.

An average two-scale simulation runs for a few tens of thousands of core hours. Thanks to allocations on supercomputers across Europe (ARCHER/UK, SuperMUC/Germany, PROMETHEUS/Poland), such highly parallel workflows are completed in a couple of days.

This work is part of the European project [ComPat](http://www.compat-project.eu/), which aims at identifying patterns in computational workflows and automate the optimisation of their execution on several, distant resources. We took part in the optimisation of computational patterns, where a "master" algorithm relies on operations performed by several instantiations of a "slave" algorithm, launched dynamically.

We use gaussian processes, in a first time, to replace partly the execution of the "slave" algorithm, in our case the nanoscale model, when after a certain number of executions the output of the algorithm given a certain input can be interpolated. Indeed, reducing drastically the computational costs. This data-driven modelling technique is performed using the [scikit-learn](http://scikit-learn.org) machine learning library. Most of the complexity is induced by the application of such regression technique to highly non-linear physics (fracture), where the features and their similarity are non-obvious.
