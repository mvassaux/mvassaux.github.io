---
layout: post
title: research projects
skip_related: true
---

** decompose in three pages, accessed in header unfolding menu under projects **

** or pop each of these pages from the figure on the main page **

** contour separately science and devs parts on each topic **

** recap links at bottom **

# Stability of concrete structures under seismic loading

## science

Accurate simulation of massive reinforced concrete structures facing cyclic loading such as containment walls in nuclear power plants during a earthquake, requires precise and stable constitutive models that can be used jointly with finite element models. One of their key features is their ability to reproduce the amount of dissipated energy partly due to fracture and partly due to mechanisms associated to oscillatory loadings.

My PhD research focused on studying and modelling concrete at two-scales: the scale of a batch of concrete and the scale of an engineering structural element. I tried to understand and model the mechanical behaviour of concrete under cyclic loading, which is inherently complicated by the closure of cracks, causing gradual regain of stiffness, but most unexpectedly hysteresis.

** figure: a cracked wall **

Using a microscopic scale model for concrete, assuming homogeneity of the constituents but explicit description of cracking and partial representativity of cracks roughness, we have explored mechanisms related to cyclic loadings. Monitoring contact and friction in formed cracks in a few centimetres large piece of concrete, we have been able to understand how internal self-balanced pre-strains, released at cracking, can generate gradual stiffness recovery and hysteresis during unloading ** cite: regul ** .

** figure: uniaxial behaviour vs. zoom on closing crack **

Well, that is set aside now, scale effects in fracture still have to be figured out.

## devs

On the development side of things, which was most of my PhD allocation, I spent my time developing the microscale model of a batch of concrete. Originally it was an existing lattice model that I extended to a particle-based model, or as we call it now a beam-particle model ** cite: beam-particle ** . In short, the continuum is discretised using Voronoï tessellation, polygonal particles are initially linked by brittle beams, and upon their failure can interact further by contact and friction. To enhance numerical stability, which was severely impaired by the simultaneous integration of brittle failure, contact and friction, I also redesigned the solution algorithm to solve quasi-static equilibrium ** cite: lattice ** . The whole code is freely available on github ** ref: github/deap ** .

Findings on the microscale mechanisms related to cracks closure led us to the formulation of a constitutive model for quasi-brittle materials cyclically loaded with enhanced numerical stability ** cite: regul ** . The model is now implemented ** ref: concyc ** and available in the open-source structural analysis and fluid mechanics software based on the finite element method developed at the CEA ** ref: cast3m ** .

# Migration of mesenchymal stem cells

## science

The behaviour of mesenchymal stem cells is driven by tremendous variety of physical cues. Among them, mechanical cues, so far proven to influence migration, differentiation, mitosis, and apoptosis. By regulating the shape of cellular constituents, mechanical cues potentially can determine the complete cellular life cycle. Some conditions have been shown to consistently promote identical cellular behaviour. For adherent cells, stiffness or spatial arrangement of the substrate are determinant. Understanding the intermediate consequences of such mechanical constraints, and finally why they promote such final behaviour, are of two main interests in cellular biology: breaking down signalling pathways and set stones of biomedical engineering.

Modelling MSCs adhesion in hemispheres, and comparing the establishment of force networks in the cytoskeleton, we have shown that cells are in lower energy state (relaxed) when found in holes instead of on bumps. Hollow areas represent more stable environments, therefore probably more suited for biological purposes such as division, which would benefit from reduced sensitivity to mechanical perturbations ** cite: paper model ** .

** figure: force networks on various curvatures **

Postulating migration induced by an off-centred position of the nucleus, we have been able to reproduce consistent migration of adherent cells on sinusoidal topographies. Simulations reproduced experiments realised by L. Pieuchot and shared within the ANR SinusSurf ** ref: sinussurf ** collaboration. In silico and in vitro, MSCs were shown to migrate toward hollow areas and, under forced migration, systematically avoiding hills ** cite: surf cells ** . 

** video: cell dribbles **

Being able to determine systematic preferences of MSCs is a first interesting step, but much remain to be explain, wether such behaviour can be explain by purely physical consideration, or wether it is an active cellular mechanism involving signalling pathways. However, establishing the relation between extracellular cues and lower scale molecular mechanisms is probably the most efficient solution to draw further insights on these behaviours.

## devs

All the required pieces of software that I used to develop the stem cell mechanical model could be found in the LMGC90 library ** ref: lmgc90 ** . The model itself was based on the tensegrity theory that describes the cytoskeleton as an assembly of load bearing beams and initially tensed cables.

# Hierarchical toughening of polymer nanocomposites

## science

Polymer and derived nanocomposites are hierarchically structured materials. Matter displays a various and specific architecture depending on the scale it is looked at. With an engineering application in mind, each of these architectures can be modified, choosing a specific polymer, or adding tailor-made particles, in order to tweak the physical properties of the resulting material.

We focus on fracture properties of polymer nanocomposites. We study how properties such as elastic modulus, strength and toughness are impacted, by structural heterogeneities at different scales. Currently, we investigate the interaction between the polymer cross-linked structure of epoxy at the nanoscale and sheets of graphene that expand up to the microscale.

## devs

Exploring the interaction between mechanisms at different scales, requires either a fine scale model extended up to the coarser scales (in space and time) and an extremely high amount of computational power, or a wise separation of scales in multiple models and still a huge amount of computational power, but reduced enough so that these models can be simulated on the world's biggest supercomputers.

At the moment, I develop a coupling library between based on the Heterogeneous Mutliscale Method, that allows to simulate a nanoscale and a microscale model concurrently ** ref: DeaLAMMPS/github ** . As such, the two models can exchange mechanical information and therefore we are able to understand how the interplay between the two scales. The coupling is achieved by transfer of homogenised strains and stresses.

** video: macroscale dogbone test and nanoscale tensile test **

At the nanoscale we have developed an all-atom model of epoxy resin and epoxy resin traversed by a graphene sheet using LAMMPS, a molecular dynamics package ** ref: lammps ** . And, at the microscale we have developed continuum two-phase model, which derives stresses at a given strain based on nanoscale simulations. Continuum mechanics equations are solved using  Deal.II, a finite element method library ** ref: deal.ii ** .

An average two-scale simulation runs for a few tens of thousands of core hours. Thanks to allocations on supercomputers across Europe (ARCHER/UK, SuperMUC/Germany, PROMETHEUS/Poland), such highly parallel workflows are completed in a couple of days.

This work is part of the European project ComPat ** ref: compat ** , which aims at identifying patterns in computational workflows and automate the optimisation of their execution on several, distant resources. We took part in the optimisation of computational patterns, where a "master" algorithm relies on operations performed by several instantiations of a "surrogate" algorithm, launched dynamically. One of the techniques used to optimise such workflow or pattern relies on gaussian processes. We intend to use Kriging to replace the execution of the "surrogate" algorithm, in our case the nanoscale model, when after a certain number of executions the output of the algorithm given a certain input can be interpolated. Indeed, reducing drastically the computational costs.
