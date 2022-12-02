---
title: 'astscript-zeropoint: A Gnuastro package for automatic estimation of zeropoint in astronomical imaging'
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
  - name: Elham Saremi
    affiliation: "2, 3"
    equal-contrib: true
  - name: Samane Raji
    equal-contrib: true
    affiliation: 4
  - name: Giulia Golini
    affiliation: "2, 3"
    equal-contrib: false
  - name: Zahra Sharbaf
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
date: 11 November 2022
bibliography: paper.bib
---





# Summary
In observational astronomy data analysis, magnitude calibration is one of the vital issues.
Because magnitude is one of the lowest-level direct measurements on image pixels to generate catalogs used in higher-level analysis (like measuring the galaxy stellar mass or spectral energy distribution fitting).
This paper introduces a newly added feature in GNU Astronomy Utilities (Gnuastro) for automating this job: `astscript-zeropoint`.
This script has many features: 1. The reference can either be an image or a catalog, 2. It runs in parallel, 3. its only relies on Gnuastro's mandatory dependencies (three very low-level and portable C-based libraries), making it portable and usable with minimal/optimal run-time resources.


# Statement of need

Estimating the zero point is crucial in calibration of image processing.
Because the measured flux of an object in our detectors depends on many factors (from the quantum efficiency of each pixel, to the transmission curve of the filter, to the optical system, to the atmosphere).
Zero point magnitude describe whole the hardware-specific which causes the difference in the magnitude of an object in differ images.
`astscript-zeropoint` is useful tool for calibrating images in astronomy.
More the details of this script are explaines in XXXXciteXXXX.
This script is created to calibrate the astronomical images in a device, based on the image or catalog of another device in Gnuastro.
It is now being used by other research groups such as [@nacho2021] [@martinez2021], to obtine the zero point of astronomical imges.

Gnuastro [@gnuastro] is free open source software with a large collection of programs and libraries that facilitates according to GNU standards for astronomical data analysis \footnote{https://www.gnu.org/savannah-checkouts/gnu/gnuastro}.
Entire Gnuastro's programs run on the command line.
Gnuastro has a very complete manual, the latest version of which is always on the website \footnote{https://akhlaghi.org/gnuastro.pdf}.


# Example

To find the zero point, it is common to use photometric systems with defined zero points such as some images or catalogs.
For example, the SDSS data can be a good reference for finding zero point in optical and 2MASS data for near infra-red images.

```bash
## Zero point based on the reference image
$ astscript-zeropoint image.fits --hdu=1 \
                      --reference=ref-img1.fits,ref-img2.fits \
                      --referencehdu=1,1 --referencezp=22.5,22.5 \
                      --aperarcsec=1.5,2,2.5,3 \
                      --magnituderange=16,18 \
                      --output=output.fits
```
```bash
## Zero point based on the reference catalog

$ astscript-zeropoint image.fits --hdu=1 \
                                 --catalog=cat.fits --cataloghdu=1 \
                                 --aperarcsec=1.5,2,2.5,3 \
                                 --magnituderange=16,18 \
                                 --output=output.fits
```


# Acknowledgements

We acknowledge contributions from Brigitta Sipocz, Syrtis Major, and Semyeong
Oh, and support from Kathryn Johnston during the genesis of this project.





# References
