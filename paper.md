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
  - name: Raul Infante-Saniz
    affiliation: 1
    equal-contrib: true
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
In observational astronomy data analysis, photometric calibration (magnitude calibration) \footnote{https://www.gnu.org/software/gnuastro/manual/html\_node/Brightness-flux-magnitude.html} is one of the vital issues.
Because magnitude is one of the lowest-level direct measurements on astronomical image pixels to generate catalogs used in higher-level analysis (like measuring the galaxy stellar mass or spectral energy distribution fitting).
Calibrating magnitude requires obtaining zero point value.
The zero point magnitude describes the hardware-specific factors and observational factors that vary the magnitude of an object from image to image.
This paper introduces a newly added feature in GNU Astronomy Utilities (Gnuastro) for automating this job: `astscript-zeropoint`.
This script has many features: 1. The reference can either be an image or a catalog, 2. It runs in parallel, 3. its only relies on Gnostic's mandatory dependencies (three very low-level and portable C-based libraries), making it portable and usable with minimal/optimal run-time resources.


# Statement of need

Estimating the zero point is crucial in calibration of astronomical image processing.
Because the measured flux of an object in our detectors depends on many factors (from the quantum efficiency of each pixel, to the transmission curve of the filter, to the optical system, to the atmosphere).
Zero point magnitude describe whole the hardware-specific which causes the difference in the magnitude of an object in differ images.
On the other hand, zero point is connection of images to a photometric system.
`astscript-zeropoint` is useful tool for calibrating astronomical images.
This script will be obtained the zero point value with aperture photometry.
More the details of this script are explains in XXXXciteXXXX.
This script is created to calibrate the astronomical images in a device, based on the image or catalog of another device in Gnuastro.
It is now being used by other research groups such as [@nacho2021] [@martinez2021], to obtain the zero point of astronomical images.

GNU Astronomy Utilities (Gnuastro) \footnote{https://www.gnu.org/software/gnuastro} [@gnuastro] is free open source software with a large collection of programs and libraries that complies with the GNU coding standards to facilitate astronomical data analysis, in the familiar Unix-like interface.
It consist of three parts, C/C++ libraries, compiled programs and executable shell scripts for higher level operations with compiled program.
All Gnuastro's programs run on the command line.
Gnuastro has a very complete manual, the latest version of which is always on the website \footnote{https://akhlaghi.org/gnuastro.pdf}.

`astscript-zeropoint` is one of the programs in Gnuastro that is recently added to it in $0.20$ version.
In this script we used many of the Gnuastro programs such as `astquery`, `asttable`, `astmkprof`, `astmkcatalog`, `astmatch` and `astfits`, that all of these are completely independent program in Gnuastro to obtained the zero point value with aperture photometry.

# Using the `astscript-zeropoint`

To find the zero point, it is common to use photometric systems with certain zero point such as some images or catalogs.
To obtain the zero point value with this script, having an image for calibration, a image or catalog as reference and aperture size are necessary.
All the steps to obtain the zero point are as follows:

1. Select the reference image or catalog and download it.
2. Download Gaia catalog with `astquery` program to obtain the coordinate of stars in input image accurately.
3. Select different aperture size with `--aperarcsec` option.
4. With `astmkprof` build an image that instead of each stars include of profile with certain aperture size.
5. Calculate the magnitude in each aperture.
6. Compare the calculated magnitude of each star between catalog of input and references in different aperture.
7. Choose the aperture that has less standard deviation as best aperture.
8. Finally consider the zero point of the best aperture as zeropoint of input image.

Example of both methods is given below if the reference be as image or a catalog.
All the steps of how using this program for two scenarios are explained in more detail in tutorial of the Gnuastro XXXXCiteXXXXX.


### Example 1: Zero point based on the reference image

If you want to obtain the zeropoint of an image (`img.fits`) based on the reference images (`refimg-1.fits` and `refimg-2.fits`) by below command the zero point will be obtain easily and output will save in the `output.fits`.

```bash
## Zero point based on the reference image
$ astscript-zeropoint img.fits --hdu=1 \
                      --reference=refimg-1.fits,refimg-2.fits \
                      --referencehdu=1,1 --referencezp=22.5,22.5 \
                      --aperarcsec=1.5,2,2.5,3 \
                      --magnituderange=16,18 \
                      --output=output.fits
```

### Example 2: Zero point based on the reference catalog ##

If you want to obtain the zero point of an image (`image.fits`) based on the reference catalog (`cat.fits`), by inserting the flollowing command line the zero point of `image.fits` will be obtained.

```bash
## Zero point based on the reference catalog
$ astscript-zeropoint image.fits --hdu=1 \
                                 --catalog=cat.fits --cataloghdu=1 \
                                 --aperarcsec=1.5,2,2.5,3 \
                                 --magnituderange=16,18 \
                                 --output=output.fits
```

# For Developers and availability
The Gnuastro manual has a full \href{https://www.gnu.org/software/gnuastro/manual/html_node/Developing.html}{chapter for developers}.
For full details please see there.
In summary Gnuastro is managed in \href{https://savannah.gnu.org/projects/gnuastro}{GNU Savannah}, which contains all necessary links (for instance to report bugs, defining tasks and etc.).

Gnuastro's source code is released under the GNU General Public License version three or above (GPLv3+) and is hosted as a \href{https://git.savannah.gnu.org/cgit/gnuastro.git}{Git repository} on Savannah.


# Acknowledgments
Authors gratefully acknowledge Ignacio Trujillo for their good advice and discussion.


# References
