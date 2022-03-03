---
title: "Islatu: A Python package for the reduction of reflectometry data"
tags:
  - Python
  - reflectometry
  - synchrotron radiation
  - condensed matter
authors:
  - name: Richard Brearton
    orcid: 0000-0002-8204-3674
    affiliation: "1, 2" # (Multiple affiliations must be quoted)
  - name: Andrew McCluskey
    orcid:
    affiliation: 2
  - name: Tim Snow
    orcid:
    affiliation: "1, 4"
affiliations:
  - name: Diamond Light Source Ltd, Diamond House, Harwell Campus, Didcot, Oxfordshire, OX11 0DE
    index: 1
  - name: Department of Physics, Clarendon Laboratory, University of Oxford, Oxford OX1 3PU, United Kingdom
    index: 2
  - name: European Spallation Source ERIC, P.O. Box 176, SE-221 00, Lund, Sweden
    index: 3
  - name: Good morning
    index: 4
date: 03 March 2022
bibliography: paper.bib
---

# Summary

The interaction between light and matter provides a sensitive probe of the
electronic structure of materials, on lengthscales determined by the difference
between the incident and outgoing wavevector of the light. Reflectometry
techniques involve scattering off the surface of a material, placing a detector
at a point such that any light reaching the detector had to scatter through a
vector approximately parallel to the material's surface normal. If the length of
this scattering vector is particularly small, there are several corrections that
must be applied to convert the raw data acquired by the detector to a quantity
proportional to the quantity of interest: the modulus squared of the scattering
matrix element ${\langle \vec{k}'\rvert}\hat{V}\lvert \vec{k} \rangle$.

<!-- The forces on stars, galaxies, and dark matter under external gravitational
fields lead to the dynamical evolution of structures in the universe. The orbits
of these bodies are therefore key to understanding the formation, history, and
future state of galaxies. The field of "galactic dynamics," which aims to model
the gravitating components of galaxies to study their structure and evolution,
is now well-established, commonly taught, and frequently used in astronomy.
Aside from toy problems and demonstrations, the majority of problems require
efficient numerical tools, many of which require the same base code (e.g., for
performing numerical orbit integration). -->

# Statement of need

`Islatu` is a python package that simplifies the process of reducing raw
reflectometry data. Errors are automatically propagated from the raw data to the
reduced dataset using optimized numpy routines[@harris2020array]. This package is designed
to serve two purposes. Firstly, it provides an interface that can be used to
easily script custom reflectometry reduction pipelines. As the fitting of
reduced reflectivity data is an ill-posed problem, it is often challenging to
fit reflectivity curves, even with significant a-priori knowledge of the
structure of the material of interest. In some cases, this could be related to
errors made at data reduction time. Islatu gives large scale facility users the
ability to script data reduction at analysis time. This can be particularly
important when combining data sets with very different statistical uncertainties
(as would be the case when comparing neutron and x-ray reflectivity curves).

The second purpose of `Islatu` is to provide a simple command-line interface,
that can be used in conjunction with a configuration file, to make reflectivity
reduction as automatic as possible. At large-scale facilities, to make the most
of valuable beamtime, it is imperative that feedback on scans is given to users
as quickly as possible after a scan has been performed.

# Overview

There are a multitude of instruments around the world capable of recording
reflectivity data. `Islatu` has been designed with this in mind, with a focus on
directly supporting international standard file formats (including the NeXus and
ORSO file formats) for the initial release, making `Islatu` compatible with most
modern synchrotrons. Thanks to `Islatu`'s modular design, it is a
straightforward task to extend this functionality to other data sources; only
one parsing function needs to be added per file type.

Islatu was designed with two-dimensional detectors in mind, but support for
point detectors is complete and all reduction steps can be carried out with
identical syntax.

<!-- `Gala` is an Astropy-affiliated Python package for galactic dynamics. Python
enables wrapping low-level languages (e.g., C) for speed without losing
flexibility or ease-of-use in the user-interface. The API for `Gala` was
designed to provide a class-based and user-friendly interface to fast (C or
Cython-optimized) implementations of common operations such as gravitational
potential and force evaluation, orbit integration, dynamical transformations,
and chaos indicators for nonlinear dynamics. `Gala` also relies heavily on and
interfaces well with the implementations of physical units and astronomical
coordinate systems in the `Astropy` package [@astropy] (`astropy.units` and
`astropy.coordinates`).

`Gala` was designed to be used by both astronomical researchers and by
students in courses on gravitational dynamics or astronomy. It has already been
used in a number of scientific publications [@Pearson:2017] and has also been
used in graduate courses on Galactic dynamics to, e.g., provide interactive
visualizations of textbook material [@Binney:2008]. The combination of speed,
design, and support for Astropy functionality in `Gala` will enable exciting
scientific explorations of forthcoming data releases from the _Gaia_ mission
[@gaia] by students and experts alike. -->

# Citations

<!-- Citations to entries in paper.bib should be in
[rMarkdown](http://rmarkdown.rstudio.com/authoring_bibliographies_and_citations.html)
format.

If you want to cite a software repository URL (e.g. something on GitHub without a preferred
citation) then you can do it with the example BibTeX entry below for @fidgit.

For a quick reference, the following citation commands can be used:

- `@author:2001` -> "Author et al. (2001)"
- `[@author:2001]` -> "(Author et al., 2001)"
- `[@author1:2001; @author2:2001]` -> "(Author1 et al., 2001; Author2 et al., 2002)" -->

# Figures

<!-- Figures can be included like this:
![Caption for example figure.\label{fig:example}](figure.png)
and referenced from text using \autoref{fig:example}.

Figure sizes can be customized by adding an optional second parameter:
![Caption for example figure.](figure.png){ width=20% } -->

# Acknowledgements

<!--
We acknowledge contributions from Brigitta Sipocz, Syrtis Major, and Semyeong
Oh, and support from Kathryn Johnston during the genesis of this project. -->

# References
