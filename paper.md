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
  - name: Samane Raji
    equal-contrib: true
    affiliation: 2
  - name: Elham Saremi
    affiliation: "3, 4"
    equal-contrib: true
  - name: Zahra Sharbaf
    affiliation: "3, 4"
    equal-contrib: true
  - name: Giulia Golini
    affiliation: "3, 4"
    equal-contrib: true
  - name: Zohreh Ghafari
    affiliation: "3, 4"
    equal-contrib: true
  - name: Mohammad Akhlaghi
    orcid: 0000-0003-1710-6613
    affiliation: 1
    equal-contrib: true
affiliations:
 - name: Centro de Estudios de Física del Cosmos de Aragón (CEFCA), Plaza San Juan 1, 44001 Teruel, Spain
   index: 1
 - name: Dept. of Theoretical and Atomic Physics, and Optics, University of Valladolid, Spain
   index: 2
 - name: Instituto de Astrofísica de Canarias, Calle Vía Láctea s/n, 38205 La Laguna, Spain
   index: 3
 - name: Departamento de Astrofísica, Universidad de La Laguna, 38205 La Laguna, Spain
   index: 4
date: 11 November 2022
bibliography: paper.bib
---





# Summary
In observational astronomy data analysis, magnitude calibration is one of the vital issue.
Because magnitude is the thing we directly measure from the image pixels and create in catalogs.
Owing to this, estimating the zero point is essential in calibration step of image processing.
Formerly, Vega star's magnitude was used as zeropoint magnitude for obtaining the standard magnitude.
But Vega star is not eternaly in the sky, and it can not be used as reference of zero point magnitude.
These days, instead of Vega’s magnitude, AB magnitude standard is used for calibration.
Gnuastro’s astscript-zeropoint script is created to obtain zero point of an image of a device based on the AB magnitude standard, based on the image or catalog of another device that overlap with original image and their zero point are known.


# Statement of need

Gnuastro [@gnuastro] is free open source software with a large collection of programs and libraries that that facilitates according to GNU standards.
for astronomical data analysis \footnote{https://www.gnu.org/savannah-checkouts/gnu/gnuastro}.
Entire Gnuastro's programs run on the command line.
Gnuastro has a very complete manual, the latest version of which is always on the website.
One of these programs is astscript-zeropoint script which is created to obtain zero point of an image in a device, based on the image or catalog of another device that overlap with original image and their zero point are known.
More the details of this script are explaines in XXXXciteXXXX.

Estimating the zero point is crucial calibration step in image processing.
Why is the zero point important?
Flux and luminosity are congenital properties of astronomical objects.
While brightness and magnitude of an object depends on the tool which object is detected.
Depending on the instrument and tools, the brightness and magnitude of an object will change.
Due to it, in observational astronomy data analysis, mostly brightness and magnitude are discussed.
The essential thing here is that the magnitude is the same as the brightness which is reported in logarithem unit.
In order to magnitude of an objecets to be dimensionless, its brightness is divided by the reference brightness.
The amount of the reference brigntness is considered to be one, therefore reference magnitude commonly known as zero point magnitude.
Zero point magnitude describe whole the hardware-specific which causes the difference in the magnitude of an object in differ images.

# Example

To find the zero point, it is common to use photometric systems with defined zero points such as some images or catalogs.
For example, the SDSS data can be a good reference for finding zero point in optical and 2MASS data for near infra-red images.

## Zero point based on the reference image

$ astscript-zeropoint image.fits --hdu=1 \
                      --reference=ref-img1.fits,ref-img2.fits \
                      --referencehdu=1,1 --referencezp=22.5,22.5 \
                      --aperarcsec=1.5,2,2.5,3 \
                      --magnituderange=16,18 \
                      --output=output.fits

## Zero point based on the reference catalog

$ astscript-zeropoint image.fits --hdu=1 \
                                 --catalog=cat.fits --cataloghdu=1 \
                                 --aperarcsec=1.5,2,2.5,3 \
                                 --magnituderange=16,18 \
                                 --output=output.fits

# Acknowledgements

We acknowledge contributions from Brigitta Sipocz, Syrtis Major, and Semyeong
Oh, and support from Kathryn Johnston during the genesis of this project.





# References
