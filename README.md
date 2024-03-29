# cueART documentation and links

`cueART` stands for Centre for Ultrasonic Engineering Acoustic Research Toolbox. 

It is a collection of modules that are related to ultrasonic signal simulation and processing. 

Initially, the following modules are provided:

#### Probe/ inspection scenario design:

* [cueBEAM](cueBEAM.md) -  A module for quick transmitted acoustic field prediction
* [cueMAP](cueMAP.md) - 2D and 3D image Point Spread Function (PSF) measurement tools, useful for probe/inspection scenario design

#### FMC to image processing:

- [cueTFM2](cueTFM2.md) - a module for transforming FMC data sets into TFM data sets (Full Matrix Capture into Total Focussing Method image)
- [SoftBscan](SoftBscan.md) - a FMC to B-scan - imaging method
- [cuePRM](cuePRM.md) - FMC to Ply Resolving Method - imaging method

#### Miscellaneous tools

* [polyfit](polyfit.md) - A module for rapid curve fitting

* [FMCSim](FMCSim.md) - a module for rapid FMC data set simulation 

#### Miscellaneous documentation
* [Data hygiene](data_hygiene.md) - data management advice


----

# cueART 0.1 API general capability sheet

The following modules are provided:

## cueBeam 

A module for transmitted acoustic field prediction. Utilizes a number of simplifications to make the calculations quick. 

assumptions: 

- The transmitters are point-like monopoles, monochromatic. That is, transmited signal is single-frequency continuous.  They are described in 3D space by xyz location, amplitude of radiation and phase of radiation. 
- The acoustic propagation medium is homogenous, single wave velocity
- The acoustic field can be gathered onto an XZ plane (rectangular sampling), or a hemisphere, using Lambert sampling.



Note, for accuracy, use another tool, e.g. https://field-ii.dk/ instead. This software is not intended to replace or compete with Field-II.

## cueMAP

A set of tools to calculate image quality metrics: focal spot size, main lobe amplitude, side lobe amplitude, and integrated energy ratio. Can be combined with `FMCSim` and `cueTFM2` to generate spatial maps of image quality for a given probe/inspection scenario.


## polyfit

A module for rapid fitting of batches of polynomial curves into supplied batches of XY points. The code is heavily optimized towards massively parallel processors, making it suitable for CUDA cards. The limitations are that the order of polynomial and the count of points is fixed per batch.

## cueTFM2

An implementation of the Total Focusing Method. Utilizes `polyfit` module to achieve very high performance. Supports arbitrarily-curved refracting interfaces - that is, the probe can be in one medium (e.g. water, wedge) and the image is calculated in another medium

## FMCSim

A very simple Full Matrix Capture signal simulator. Originally intended to support the debugging of `cueTFM2` code, but also useful for `cuePRM`, `cueMAP` and general demonstrations.

## SoftBscan

A software-defined B-scan from FMC processor. Supports linear (1D) probes only (generating a 2D image). Supports azimuthal scan, and Dynamic Depth Focussing. No refraction.

## cuePRM

Implementation of the Ply Resolving Method 

##### cuePRMBasic

​	integrates the at-pixel paths only

##### cuePRMFull

​	integrates all paths fitting a provided criterion into a given pixel

# Contributing

This particular instance of repository is for a stable, usable version of the software only.  Since many of the modules here depend in this or another way on others, we want to avoid the "dll hell" scenario.

For development, please clone this repository, add Your changes there, use them, document them, and then submit Your version for consideration of one of the core authors.



# License



![CC](resources/cc-icons-png/cc.png) ![BY](resources/cc-icons-png/by.png) ![SA](resources/cc-icons-png/sa.png) ![Free Culture](resources/cc-icons-png/seal.png)

This work is shared under `Creative Commons` [Attribution-ShareAlike 4.0 International](https://creativecommons.org/licenses/by-sa/4.0/)  license, which is a [Free Culture](https://creativecommons.org/share-your-work/public-domain/freeworks) License. In short, you can use it, even for Your work, and even encapsulate the verbatim version inside closed commercial packages, but any modifications must be shared for free. 

Also, we trust for You to not be naughty by forgetting to mention the contributors.



# Contributor list

Dr Jerzy Dziewierz

Dr Timothy Lardner

Marcus Ingram

Dr Carmelo Mineo

Riliang Su

Dr Yashar Javadi 

Dr Anthony Gachagan

If You contributed in any way, and you are not listed here - please let me know, I will surely honor Your contribution.




## Contributing
1. For version number, use semantic verisioning 2.0.0 : https://semver.org/
2. For branching workflow, use this: http://nvie.com/posts/a-successful-git-branching-model/
3. For documentation, use this: http://www.writethedocs.org/guide/writing/beginners-guide-to-docs/
4. For new features, start a new folder, then a new submodule, and then use this: http://tom.preston-werner.com/2010/08/23/readme-driven-development.html
4. For anything else, ask Jerzy Dziewierz


