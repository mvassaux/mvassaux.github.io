---
layout: post
title: Migration of mesenchymal stem cells
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

The behaviour of mesenchymal stem cells is driven by tremendous variety of physical cues. Among them, mechanical cues, so far proven to influence migration, differentiation, mitosis, and apoptosis. By regulating the shape of cellular constituents, mechanical cues potentially can determine the complete cellular life cycle. Some conditions have been shown to consistently promote identical cellular behaviour. For adherent cells, stiffness or spatial arrangement of the substrate are determinant. Understanding the intermediate consequences of such mechanical constraints, and finally why they promote such final behaviour, are of two main interests in cellular biology: breaking down signalling pathways and set stones of biomedical engineering.

Modelling MSCs adhesion in hemispheres, and comparing the establishment of force networks in the cytoskeleton, we have shown that cells are in lower energy state (relaxed) when found in holes instead of on bumps. Hollow areas represent more stable environments, therefore probably more suited for biological purposes such as division, which would benefit from reduced sensitivity to mechanical perturbations [[1]](#pstem).

**figure: force networks on various curvatures**

Postulating migration induced by an off-centred position of the nucleus, we have been able to reproduce consistent migration of adherent cells on sinusoidal topographies. Simulations reproduced experiments realised by L. Pieuchot and shared within the [ANR-SinusSurf](http://www.agence-nationale-recherche.fr/Project-ANR-12-BSV5-0010) collaboration. In silico and in vitro, MSCs were shown to migrate toward hollow areas and, under forced migration, systematically avoiding hills [[2]](#psinus).

<iframe src="https://drive.google.com/file/d/0B4RDr7FXP4QHNE9uamZLMXlJbDQ/preview" width="450" height="300"></iframe>

<!-- Do montage with the experimental observation and gif of the movie! -->

<!-- <video width="400" controls>
  <source src="../../static/neymar.m4v" type="video/m4v">
  Your browser does not support HTML5 video.
</video> -->
Being able to determine systematic preferences of MSCs is a first interesting step, but much remain to be explain, wether such behaviour can be explain by purely physical consideration, or wether it is an active cellular mechanism involving signalling pathways. However, establishing the relation between extracellular cues and lower scale molecular mechanisms is probably the most efficient solution to draw further insights on these behaviours.

## developments
{: name="devs"}

All the required pieces of software that I used to develop the stem cell mechanical model could be found in the [LMGC90](https://git-xen.lmgc.univ-montp2.fr/lmgc90/lmgc90_user/wikis/home) library. The model itself was based on the tensegrity theory that describes the cytoskeleton as an assembly of load bearing beams and initially tensed cables.

## publications
{: name="publications"}

[1] Maxime Vassaux and Jean-Louis Milan.<br>[*Stem cell mechanical behaviour modelling: substrate’s curvature influence during adhesion.*](https://doi.org/10.1007/s10237-017-0888-4)<br>Biomechanics and modeling in mechanobiology, 16 (2017): 1295-1308.
{: id="pstem"}

[2] Laurent Pieuchot, Maxime Vassaux, Julie Marteau, Thomas Cloatre, Tatania Petithory, Isabelle Brigaud, Pierre-François Chauvy, Arnaud Ponche, Jean-Louis Milan, Pablo Rougerie, Maxence Bigerelle, and Karine Anselme.<br>*Curvotaxis directs cell migration through cell-scale curvature landscapes.*<br>Nature Materials, (2018): *in review*.
{: id="psinus}
