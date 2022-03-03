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
    affiliation: 3
  - name: Tim Snow
    orcid:
    affiliation: "1, 4"
affiliations:
  - name: Diamond Light Source Ltd, Diamond House, Harwell Campus, Didcot, Oxfordshire, OX11 0DE, United Kingdom
    index: 1
  - name: Department of Physics, Clarendon Laboratory, University of Oxford, Oxford, Oxfordshire, OX1 3PU, United Kingdom
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
vector approximately parallel to the material's surface normal. Typically, for
various experiment-specific reasons, the raw data recorded by a detector will
not be proportional to the quantity of interest: the modulus squared of the
scattering matrix element
${\langle \vec{k}'\rvert}\hat{V}\lvert \vec{k} \rangle$. This is particularly
true when the length of the scattering vector
$|\vec{Q}| = |\vec{k} - \vec{k}'|$
is small, as is the case in reflectivity experiments. Then, in addition to
corrections that must be applied in any scattering experiment, the finite
size of the sample will affect the intensity of the
reflected beam, and it is often necessary to also correct for manual changes
to the beam's attenuation.

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

`Islatu` is a Python package that simplifies the process of reducing raw
reflectometry data. Errors are automatically propagated from the raw data to the
reduced dataset using optimized `numpy` routines [@harris2020array]. This package
is designed
to serve two purposes. Firstly, it provides an interface that can be used to
easily script custom reflectometry reduction pipelines. As the fitting of
reduced reflectivity data is an ill-posed problem, it is often challenging to
fit reflectivity curves, even with significant a-priori knowledge of the
structure of the material of interest. In some cases, this could be related to
errors made at data reduction time. Islatu gives large scale facility users the
ability to script data reduction at analysis time. This can be particularly
important when combining data sets with very different statistical uncertainties
(as would be the case when comparing neutron and x-ray reflectivity curves), as
errors are computed at data reduction time.

The second purpose of `Islatu` is to provide a simple command-line interface,
that can be used in conjunction with a configuration file, to make reflectivity
reduction as automatic as possible. At large-scale facilities, to make the most
of valuable beamtime, it is imperative that feedback on scans is given to users
as quickly as possible after a scan has been performed.

# Overview

There are a multitude of instruments around the world capable of recording
reflectivity data. `Islatu` has been designed with this in mind, with a focus on
directly supporting international standard file formats (including the NeXus
[@konnecke2015nexus] and ORSO file formats) for the initial release,
making `Islatu` compatible with most
modern synchrotrons. Thanks to `Islatu`'s modular design, it is a
straightforward task to extend this functionality to other data sources; only
one parsing function needs to be added per file type.

Islatu was designed for use with two-dimensional detectors, but support for
point detectors is complete and all reduction steps can be carried out with
identical syntax. To give an overview of `Islatu`'s Python API, the first step
in any data reduction with `Islatu` is to instantiate a `Profile` object. A full
reflectivity profile can generally be made up of more than one
$|\vec{Q}|$
scan, where $\vec{Q}$ is the probe particle's
scattering vector. To instantiate a `Profile` object, all that needs to be
provided is a list of source files and a function that can be used to parse
them. Once the profile has been instantiated, reduction takes place by calling
the `Profile` object's methods. For example, for an instance of `Profile`
named `my_profile` representing data acquired when a beam with a full width at
half maximum of 100 $\mu$m incident on a sample of length 10 mm, our
reflectometry profile can be footprint corrected by calling
`my_profile.footprint_correction(beam_width=100e-6, sample_size=10e-3)`.
The footprint correction is
exact for Gaussian beam profiles, and, along with all other reduction methods
available to `Profile` objects, propagates errors optimally (such that the
number of mathematical operations required to propagate the errors is
minimized). The other reduction methods can be used in entirely analogous ways,
taking arguments where necessary, and using metadata scraped from the raw data
files wherever possible.

As well as the abovedescribed Python API, `Islatu` also features a command-line
interface. This application is used at the I07 beamline at Diamond
[@nicklin2016diamond]
to process reflectivity data immediately after acquisition. The command-line
interface runs a typical `Islatu` processing script, where the arguments taken
by the various data reduction methods in the script are extracted from a combination
of a .yaml configuration file and command-line arguments. The program outputs a
human-readable metadata-rich .dat file, which at present aims to comply with the
ORSO .ort file format definition, and will be converted to comply exactly with
the .ort file format at such a time as the ORSO file format specification is
finalized.

# Acknowledgements

We acknowledge the support of Ada Lovelace Centre and what not.

# References
