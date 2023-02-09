---
title: 'astscript-zeropoint: a Gnuastro script to estimate the zero point of astronomical images'
tags:
  - Gnuastro
  - astronomy
  - zeropoint
authors:
  - name: Sepideh Eskandarlou
    orcid: 0000-0002-6672-1199
    corresponding: true
    equal-contrib: true
    affiliation: 1
  - name: Raúl Infante-Sainz
    orcid: 0000-0002-6220-7133
    affiliation: 1
    equal-contrib: true
  - name: Elham Saremi
    affiliation: "2, 3"
    equal-contrib: true
  - name: Samane Raji
    equal-contrib: true
    affiliation: 4
  - name: Zahra Sharbaf
    affiliation: "2, 3"
    equal-contrib: false
  - name: Giulia Golini
    affiliation: "2, 3"
    equal-contrib: false
  - name: Zohreh Ghafari
    affiliation: "2, 3"
    equal-contrib: false
  - name: Mohammad Akhlaghi
    orcid: 0000-0003-1710-6613
    affiliation: 1
    equal-contrib: true
affiliations:
 - name: Centro de Estudios de Física del Cosmos de Aragón (CEFCA), Plaza San Juan 1, 44001 Teruel, Spain
   index: 1
 - name: Instituto de Astrofísica de Canarias, Calle Vía Láctea s/n, 38205 La Laguna, Spain
   index: 2
 - name: Departamento de Astrofísica, Universidad de La Laguna, 38205 La Laguna, Spain
   index: 3
 - name: Dept. of Theoretical and Atomic Physics, and Optics, University of Valladolid, Spain
   index: 4
date: 6 January 2023
bibliography: paper.bib
---





# Summary
The photometric calibration (zero point magnitude estimation) is a fundamental step in astronomical data analysis.
The zero point magnitude is the connection between the observed data with a photometric system.
It encodes all the instrument-specific and observational factors into a single value that allows the use of the data for higher-level analysis (e.g., measuring the galaxy stellar masses or spectral energy distribution fitting).
This paper introduces a newly added script in GNU Astronomy Utilities (Gnuastro) for automating this job: `astscript-zeropoint`.
This script has many features: 1. The reference dataset can be either an image or a catalog, 2. It runs in parallel, 3. Its few dependencies makes it portable and usable with minimal/optimal run-time resources.


# Introduction
Useful measurements of astronomical sources are not possible without the reduction and the calibration of the raw data.
The estimation of the zero point consists in making the connection between the observed data to a standard photometric system.
After that, the measured values like fluxes, brightness, and other parameters have physical meaning and can be compared with other measurements from different telescopes and instruments.

Here we introduce a new script in charge of computing the zero point magnitude of astronomical images: `astscript-zeropoint`.
It performs the aperture photometry of the objects and compares them with already calibrated datasets (images or catalog).
This script belongs to GNU Astronomy Utilities (Gnuastro) \footnote{https://www.gnu.org/software/gnuastro} [@gnuastro2015; @gnuastro2019] since Gnuastro version $0.20$.
This script is now being used by other research groups such as @trujillo2021 and @martinez2021 to obtain the zero point of their astronomical images.


# Computing the zero point with `astscript-zeropoint`
Prior to the use of this script, it is necessary to collect the reference images or catalog.
This reference data is used as the basis to compare the aperture photometry done by the script.
The basic steps performed internally by the script:

1. Download Gaia catalog to obtain accurate coordinates of stars on the input image.
2. Perform aperture photometry considering different aperture sizes (option `--aperarcsec`).
3. For each aperture size, compute the difference in magnitude with respect to the reference data.
4. Compute the zero point magnitude as the robust averaged difference between the magnitudes.
5. Finally, select the zero point from the aperture size that provides the smaller standard deviation.

Depending on the reference data, images or a catalog, the way of using the script is a bit different.
But in practice, the essence is the same.
In what follows, we expose two examples on how to invoke the script in order to obtain the zero point magnitude of an image.


### Example 1: Zero point based on reference images
Obtain the zero point of an image (`img.fits`) based on reference images (`refimg-1.fits` and `refimg-2.fits`) that overlap with `img.fits`.
In this case, the reference images have zero points of 22.5 mag each.
Consider 4 different apertures of 1.5, 2, 2.5, and 3 arcsec.
Use objects within the range of magnitude from 16 to 18 mag.
Save the result as `output.fits`.

```bash
$ astscript-zeropoint img.fits --hdu=1 \
                      --refimgs=ref-image-1.fits,ref-image-2.fits \
                      --refimgshdu=1,1 --referencezp=22.5,22.5 \
                      --aperarcsec=1.5,2,2.5,3 \
                      --magnituderange=16,18 \
                      --output=output.fits
```


### Example 2: Zero point based on a reference catalog
Obtain the zero point of an image (`img.fits`) based on a reference catalog (`cat.fits`) whose objects overlap with `img.fits`.
In this case, the reference is a catalog of objects.
Consider 4 different apertures of 1.5, 2, 2.5, and 3 arcsec.
Use objects within the range of magnitude from 16 to 18 mag.
Save the result as `output.fits`.

```bash
$ astscript-zeropoint image.fits --hdu=1 \
                      --refcat=cat.fits --refcathdu=1 \
                      --aperarcsec=1.5,2,2.5,3 \
                      --magnituderange=16,18 \
                      --output=output.fits
```


# Further information
More details and information including a full step by step tutorial on how to use this script can be found in the official documentation of Gnuastro.
The latest version is always on the website \url{https://akhlaghi.org/gnuastro.pdf}.
Gnuastro's source code is released under the GNU General Public License version three or above (GPLv3+) and is hosted as a \href{https://git.savannah.gnu.org/cgit/gnuastro.git}{Git repository} on Savannah.


# Acknowledgements
We acknowledge Ignacio Trujillo for the good advice and discussions that improved the script.


# References
