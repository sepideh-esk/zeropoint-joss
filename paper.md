---
title: 'astscript-zeropoint: a Gnuastro script to estimate the zero point magnitude of astronomical images'
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
    orcid: 0000-0002-5075-1764
    affiliation: "2, 3"
    equal-contrib: true
  - name: Samane Raji
    orcid: 0000-0001-9000-5507
    equal-contrib: true
    affiliation: 4
  - name: Zahra Sharbaf
    orcid: 0000-0002-0662-096X
    affiliation: "2, 3"
    equal-contrib: false
  - name: Giulia Golini
    orcid: 0009-0001-2377-272X
    affiliation: "2, 3"
    equal-contrib: false
  - name: Zohreh Ghaffari
    orcid: 0000-0002-6467-8078
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
Calibraion of pixel values is a fundamental step in astronomical image analysis.
In astronomical jargon this is known as estimating zero point magnitude.
This paper introduces a newly added script in GNU Astronomy Utilities (Gnuastro) for the zero point magnitude estimation, named: `astscript-zeropoint`.
This script has many features, including: 1. The reference dataset can be either an image or a catalog, 2. The steps are parallized to decrease the run-time to be efficient in large reduction pipelines, 3. Due to Gnuastro's minimal set of dependencies, it is flexible and portable.


# Introduction
Scientific measurements of astronomical sources are not possible without reduction and the calibration of the raw data.
The zero point magnitude allows the conversion of the observed data (pixel values) to physical units\footnote{\url{https://www.gnu.org/software/gnuastro/manual/html_node/Brightness-flux-magnitude.html}}.
The zero point magnitude encodes all the instrument-specific and observational factors, that are necessary for calibration, into a single value.
Therefore, measurements like flux, brightness, and other parameters can be compared with other measurements from different telescopes and instruments.
This allows the use of the data for higher-level analysis (for instance, measuring the galaxy's stellar masses or spectral energy distribution fitting).


Here we introduce a new script in charge of computing the zero point magnitude of astronomical images with the executable name of `astscript-zeropoint`.
It performs aperture photometry of stars in the image and compares them with already calibrated datasets (images or catalog).
This script is a new component of GNU Astronomy Utilities, or Gnuastro\footnote{\url{https://www.gnu.org/software/gnuastro}} [@gnuastro2015; @gnuastro2019] since Gnuastro version $0.20$.
Earlier versions of this script have been used by other research projects such as @trujillo2021 and @martinez2021 to obtain the zero point of their astronomical images.


# Computing the zero point magnitude with `astscript-zeropoint`
This script requires reference image(s) or a catalog that overlap with your input image.
This reference data is used as the basis to compare the aperture photometry done by the script.
The basic steps performed internally by the script are:

1. Query the Gaia\footnote{Gaia is a mission by the European Space Agency for cataloging positions, distances, motion and spectra of stars in Milky Way. For more information, see \url{https://www.esa.int/Science_Exploration/Space_Science/Gaia}.} catalog to obtain accurate coordinates of stars in an input image.
2. Perform aperture photometry considering different aperture sizes.
3. For each aperture and each star, compute the difference in magnitude with respect to the reference ($\delta_{a,s}$).
Setting the input zero point magnitude to zero.
4. Compute the zero point magnitude for each aperture ($z_a$) from the sigma-clipped median of the $\delta_{a,s}$ distribution for all stars in the desired magnitude range with the same aperture.
5. The final zero point magnitude is the $z_a$ with smallest scatter (sigma-clipped standard deviation of the $\delta_{a,s}$ distribution).

Depending on the reference data (images or a catalog), the execution of the script is slightly different; the difference is just to identify the input format.
In what follows, we expose two examples of invoking the script to obtain the zero point magnitude of an image.


### Example 1: Zero point magnitude estimation based on reference images
The zero point magnitude of an image (`img.fits`) is obtained based on reference images (`refimg-1.fits` and `refimg-2.fits`) that overlap with `img.fits`.
In this case, both reference images have zero point of 22.5 magnitude.
Four different apertures of radii 1.5, 2, 2.5, and 3 arc seconds are considered.
Objects within the range of magnitude from 16 to 18 magnitudes are used.
The result is saved as a fits file named: `output.fits`.

```bash
$ astscript-zeropoint img.fits --hdu=1 \
                      --refimgs=ref-image-1.fits,ref-image-2.fits \
                      --refimgshdu=1,1 --refimgszp=22.5,22.5 \
                      --aperarcsec=1.5,2,2.5,3 \
                      --magnituderange=16,18 \
                      --output=output.fits
```

A complete tutorial containing this scenario is available in the "Zero point tutorial with reference image"\footnote{\url{https://www.gnu.org/software/gnuastro/manual/html_node/Zero-point-tutorial-with-reference-image.html}} section of the Gnuastro manual.

### Example 2: Zero point magnitude estimation based on a reference catalog
The zero point magnitude of an image (`img.fits`) is obtained based on a reference catalog (`cat.fits`) whose objects overlap with the input.
The aperture sizes, magnitude range of objects, and output name are the same as Example 1.

```bash
$ astscript-zeropoint image.fits --hdu=1 \
                      --refcat=cat.fits --refcathdu=1 \
                      --aperarcsec=1.5,2,2.5,3 \
                      --magnituderange=16,18 \
                      --output=output.fits
```

A complete tutorial containing this scenario is available in the "Zero point tutorial with reference catalog"\footnote{\url{https://www.gnu.org/software/gnuastro/manual/html_node/Zero-point-tutorial-with-reference-catalog.html}} section of the Gnuastro manual.



# Further information
More details and complete information (including two full step-by-step tutorials on how to use this script and the concepts behind it) can be found in the respective section\footnote{\url{https://www.gnu.org/software/gnuastro/manual/html_node/Zero-point-estimation.html}} official documentation of Gnuastro.
Gnuastro's source code is released under the GNU General Public License version three or above (GPLv3+) and is hosted as a \href{https://git.savannah.gnu.org/cgit/gnuastro.git}{Git repository} on Savannah.
For installation instructions see the "Quick start" section\footnote{\url{https://www.gnu.org/software/gnuastro/manual/html_node/Quick-start.html}} of the Gnuastro manual.
For questions, comments or bug reports contact `bug-gnuastro@gnu.org` or fill support form\footnote{\url{https://savannah.gnu.org/support/?group=gnuastro&func=additem}} on Savannah.

# Acknowledgements
We gratefully acknowledge Ignacio Trujillo for the good advice and discussions that improved the script.

This work is part of GNU Astronomy Utilities (Gnuastro, ascl.net/1801.009) version 0.20. Work on Gnuastro has been funded by the Japanese Ministry of Education, Culture, Sports, Science, and Technology (MEXT) scholarship and its Grant-in-Aid for Scientific Research (21244012, 24253003), the European Research Council (ERC) advanced grant 339659-MUSICOS, the Spanish Ministry of Economy and Competitiveness (MINECO, grant number AYA2016-76219-P) and the NextGenerationEU grant through the Recovery and Resilience Facility project ICTS-MRR-2021-03-CEFCA.
We also acknowledge financial support from the ACIISI, Consejería de Economía, Conocimiento y Empleo del Gobierno de Canarias and the European Regional Development Fund (ERDF) under grant with reference PROID2021010044, and from IAC project P/300724, financed by the Ministry of Science and Innovation, through the State Budget and by the Canary Islands Department of Economy, Knowledge and Employment, through the Regional Budget of the Autonomous Community.

# References
