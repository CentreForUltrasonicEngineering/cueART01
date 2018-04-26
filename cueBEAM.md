cueBEAM - package within cueART - documentation

------

"The purpose of computer simulations is to reduce the total cost of doing the job, not to increase it" - Richard O'Leary, c.a. 2011

----



## Introduction - why cueBeam?

As of 2018, we really do not know what reality REALLY is - as far as we know, we might never know. But, we can make models. The usefullnes of the models is that they can help to explain the past and predict the future.

Models range from simple, empirical closed-form equations like Newton's "Force=Mass*acceleration" , through to finite-element models (FEM) that require equation-solving with millions of unknowns. Accuracy, and therefore the usefulness of many of the models, are often compute bound. A more accurate solution can be produced at the cost of performing a greater number of computations. However, these computations bear a cost in terms of hardware, energy and, most importantly, time.  Hence, there still exists a market for building simplified models of reality; ones that capture just enough of the complexity of real phenomena, but at the same time, are computably affordable.

## cueBeam model of the world

cueBEAM is an implementation of continuous-wave (monochromatic, single-frequency) form of the Huygens principle of wave propagation in homogenous media. 

Consider a dimensionles, omnidirectional monopole wave radiator emitting a continious wave at frequency f, phase phi, amplitude U0. In the media of wave velocity v, the radiator produces a stationary disturbance of wavelength lambda, and wavenumber k. The wave produced can be described at any time t and point r in space as a complex amplitude, decaying proportionally to the area of the sphere of the radius R:

![](cueBEAM-resources\fundamental_equation.png)



Assuming that the medium of interest is a linear, non-viscous liquid and using the principle of superposition, the amplitude of the wave stemming from multiple sources of known amplitudes and phases can be calculated as a complex sum of the contributions. 

## Intended Application

cueBeam is intended for simulation of single-way ultrasonic radiation of a phased array probe. Emphasis is placed on supporting any probe geometry, including sparse 2D array probe configurations. Probe's element directivity can be simulated by representing it with multiple point-like transmitters. 

**Using the core functionality, the following additional tasks can be performed:**

Frequency-dependent phenomena can be simulated by compounding simulations of effects at indyvidual frequency. 

Time-domain  response can be calculated by encoding the excitation signal into frequency domain using FFT, then performing calculation for indyvidual frequencies, and then using IFFT to obtain the time domain signal from the cueBeam result.

##  Implementation overview

The software has been originally written as a MEX plug-in for MATLAB, and comes in two versions: CPU(OpenMP) or  CUDA for the computation kernel. The algorithm is decomposed in such a way that each thread of the GPU or OpenMP calculates the pressure value for a single-point in space only. This allows all the computations to progress in parallel, as the pressure in space is completely and solely defined by the properties of the radiators and the media. There is no need for communication between the threads.

The following inputs are required:

* Description of the radiating points: location,amplitude and phase of radiation;
* Description of the propagation media:wavenumber;
* Description of the points in space to calculate the resulting acoustic pressure.

The algorithm can be described in pseudo-code, as follows:

~~~~
	For each pixel 
		Initialize pressure=complex zero;
		For each radiator
			Distance=distance(radiator,pixel);
			Phase shift= wavenumber*distance+radiator phaseshift;
			Amplitude decayed=radiatoramplitude/distance;
			pressure=pressurecomplex(amplitudedecayed, phase shift);
        End for each radiator
        Output(pixel)=pressure;  
	End for each pixel
~~~~



## Demos

Please note that essentially, only the core calculation module is supported. It is up to the user to make the it useful to himself.

###  ArrayEdit3: Sparse array editor

A sparse array CAD package has been built to facilitate the exploration of sparse array element layouts. This package allows for the placing and moving of the array elements defined over a triangular grid. The performance of the resulting element in terms of main lobe width and side lobe amplitude is recalculated and updated interactively as the elements are added, modified and removed. 
An example screenshot of the editor in use is presented in figure below (densely packed array) and another (sparse array). These two figures exemplify an exploration of the problem space in placing the elements on a triangular grid. In the first figure, the elements that cover six triangles are densely placed. In the second, the elements that cover 12 triangles are sparsely placed. The beam width is narrower for the sparse array, however the side lobe level is higher (the contrast is worse).

![Densely packed 122 element phased array layout defined over triangular grid in the ArrayEdit3 software package](cueBEAM-resources\ArrayEdit_dense.png)

![Screenshot of the ArrayEdit application with a probe design loaded. Array elements have been manually placed. Note the changed performance figures compared to the previous case:: narrower beam width and higher side lobe amplitude for the sparse array case](cueBEAM-resources\ArrayEdit_sparseFan.png)



### BeamDemo:Interactive beam forming and focussing demonstration

A software package has been built to interactively demonstrate the effects of changing the probe aperture, bandwidth, element count and the steering and focussing on the beam shape and image quality metrics. An example screenshot is presented in below.
The scene settings and the probe itself are defined by means of a Matlab script. 
The three main displays are interactively updated. The XZ cross-section display is a 2D slice of the 3D space defined by plane y=0. The hemisphere display is a 2D slice of the 3D space, defined by a hemisphere of radius as dictated in the settings.  Both of these displays present the calculated relative amplitude of the pressure field generated by the probe. They are also used to visualise the location of a curve (semicircle, white in the figure) that is used as a final 1D cross-section of the beam. The pressure sampled at the location along this curve is displayed in the bottom plot.
Based on the 1D cross-section, example beam characteristics are calculated: main lobe width (planar angle, width of the -3dB envelope) and leakage factor (ratio of the energy outside the main lobe to the total signal energy in the measurement plane).
The user can click the XZ or hemisphere images to direct and focus the beam at that point, instantly updating the display. Keyboard shortcuts are used to modify probe characteristics, such as to make it bigger or smaller or to change the radiation frequency.

![Example screenshot of cueBeam demonstrator. Top: two 2D cross-sections through 3D space; Lambert equiareal mapped hemisphere (top) and XZ plane (middle). Bottom – 1D cross-section of the beam along the white curve presented in the top views. From this last view, two beam characteristics are instantly calculated: main lobe width and energy leakage factor.](cueBEAM-resources\cueBeamDemo_sections.png)

