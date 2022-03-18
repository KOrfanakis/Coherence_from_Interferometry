# Calculating the Temporal Decay of *g*<sup>(1)</sup>(*t*) Using Python

<p align="center">
    <a href="https://nbviewer.org/github/KOrfanakis/Coherence_from_Interferometry/blob/main/Analysis.ipynb">
        <img alt="Render With" src="https://img.shields.io/badge/Render%20with-nbviewer-red.svg">
    </a>
    <a href="https://www.python.org/">
        <img alt="Made with" src="https://img.shields.io/badge/Made%20with-Python-blue.svg">
    </a>
    <a href="https://jupyter.org/try">
        <img alt="Made with and" src="https://img.shields.io/badge/And%20-Jupyter-orange.svg">
    </a>
    <a href="https://opensource.org/licenses/MIT">
        <img alt="Licence" src="https://img.shields.io/badge/License-MIT-0298c3.svg">
    </a>
    <a>
        <img alt="Star if useful" src="https://img.shields.io/static/v1?label=%F0%9F%8C%9F&message=If%20Useful&style=style=flat&color=9cf">
    </a>
    <br/>
</p>


**Table of Contents**:

<!--ts-->

- [Objective](#objective)
- [The Experiment](#the-experiment)
- [Data Format](#data-format)
- [Requirements](#requirements)

<!--te-->

<br>

## Objective

This repository aims to demonstrate how to extract the fringe contrast from an interferogram and calculate the temporal decay of the first-order correlation function *g*<sup>(1)</sup>(*t*).
The code was developed by [Konstantinos Orfanakis](https://scholar.google.co.uk/citations?user=U5drfBUAAAAJ&hl=en&oi=ao) and [Dr Hamid Ohadi](https://scholar.google.co.uk/citations?user=x6E7md4AAAAJ&hl=en) at the University of St Andrews and was extensively used for our first publication ([Phys. Rev. B 103, 235313 (2021)](https://journals.aps.org/prb/abstract/10.1103/PhysRevB.103.235313)).

<br>

## The Experiment

This experiment investigates the temporal coherence of an optically trapped exciton-polariton condensate. 
For this purpose, we utilise a Michelson interferometer in the mirror-retroreflector configuration (See Fig. 1). 
By varying the position of the moving arm (where a retroreflector is used for reflecting the beam) and superimposing the image from each arm, we form interferograms for various time delays.

<br>

<p align="center">
  <img src="Images/Figure 1.png" width="300" title="hover text">
</p>
<p align="center">
  <em>Figure 1: Schematic of the interferometer setup.</em>
</p>

<br>

A line profile in the centre of the interferogram can be fit by a Gaussian function (the condensate mode profile) multiplied by a cosine to acquire the fringe contrast (see Fig. 2). The exact equation is the following:

<img src="https://latex.codecogs.com/svg.latex?f(x;&space;A,&space;x_{0},&space;w,&space;\alpha,&space;k,&space;\phi,&space;ct&space;)&space;=&space;A&space;\cdot&space;exp(-\frac{(x&space;-&space;x_{0})^{2}}{2w^{2}})\cdot&space;(\alpha&space;\cdot&space;cos(k\cdot&space;x&space;&plus;&space;\phi)&space;&plus;&space;1)&space;&plus;&space;ct" title="f(x; A, x_{0}, w, \alpha, k, \phi, ct ) = A \cdot exp(-\frac{(x - x_{0})^{2}}{2w^{2}})\cdot (\alpha \cdot cos(k\cdot x + \phi) + 1) + ct" />

Where parameters *A*, *x*<sub>0</sub>, and *w* are the amplitude, the centre, and the width of the Gaussian, respectively. The parameter α corresponds to the fringe contrast, *k* to the wavenumber, φ to the phase, and *ct* to a constant.

<br>

<p align="center">
  <img src="Images/Figure 2.png" width="600" title="hover text">
</p>
<p align="center">
  <em>Figure 2: (a) Example of an interferogram. (b) Horizontal line profile across the white dashed line of the interference pattern in (a). The orange line shows the theoretical fit.</em>
</p>

<br>

The fringe contrast is equal to the magnitude of the first-order correlation function |*g*<sup>(1)</sup>(*t*)|, where *t* is the time delay.

To acquire the temporal dependence of the correlation function, we record the fringe contrast while changing the time delay. We average over several (usually five) realisations for each time delay.

<br>

## Data Format

The experimental data are saved in the [Hierarchical Data Format](https://www.hdfgroup.org/solutions/hdf5/) (HDF) as H5 files. Each interferogram is saved as a separate frame in this H5 file. A frame contains a 2D array corresponding to the interferogram image plus some extra information, called attributes (e.g. position of the moving arm, the exact time of the measurement, etc.).

In our case, we are only interested in the 2D image and the position of the moving arm. A pythonic interface to the HDF data format is provided by the [h5py package](https://docs.h5py.org/en/stable/).

Due to its size (105 MB), the file used in this tutorial cannot be uploaded on GitHub. It accessible through [Dropbox](https://www.dropbox.com/s/qhfjxkqx796g0u2/Interference_Data.h5?dl=0). The dataset used for [Phys. Rev. B 103, 235313 (2021)](https://journals.aps.org/prb/abstract/10.1103/PhysRevB.103.235313) is available through the [University of St Andrews](https://risweb.st-andrews.ac.uk/portal/en/datasets/ultralong-temporal-coherence-in-optically-trapped-excitonpolariton-condensates-dataset(cb6784fd-521e-46c6-a4fa-c8936cab4f4b).html).

<br>

## Requirements

Python Version: 3.10.2  <br>
Jupyter Notebook Version: 6.4.8 <br>
Packages: h5py (3.6.0), NumPy (1.22.2), Matplotlib (3.5.1), LMfit (1.0.3), SciPy (1.8.0), Pandas (1.4.1), tqdm (4.62.3)
