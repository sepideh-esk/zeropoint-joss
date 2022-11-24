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
  - name: Zohre Ghafari
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
Estimating the zero point is crucial calibration step in image processing.
Moreover, zero point is essential to calibrate magnitude to standard magnitude.
More details are fully explained in \url{https://www.gnu.org/savannah-checkouts/gnu/gnuastro/manual/gnuastro.html#Brightness-flux-magnitude}.
Formerly, Vega star's magnitude was used as zeropoint magnitude for obtaining the standard magnitude.
But Vega star is not eternaly in the sky, and it can not be used as reference of zero point magnitude.
Predominantly, any star that is in the sky can be used to obtain the zero point by using its apparent magnitude.

Gnuastro’s @command{astscript-zeropoint} script is created to obtain zero point of an image of a device, based on the
 image or catalog of another device that overlap with original image and their zero point are known.



# Statement of need

Gnuastro [@gnuastro] is a large collection of programs and libraries
for astronomical data analysis.





# Acknowledgements

We acknowledge contributions from Brigitta Sipocz, Syrtis Major, and Semyeong
Oh, and support from Kathryn Johnston during the genesis of this project.





# References
