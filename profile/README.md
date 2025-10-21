# CMB-ML: A Cosmic Microwave Background Radiation Dataset for Machine Learning

The Cosmic Microwave Background radiation (CMB) signal is one of the cornerstones upon which modern cosmologists understand the universe. The signal must be separated out from other natural phenomena which either emit microwave signals or affect the CMB signal itself. Modern machine learning and computer vision algorithms are seemingly perfect for the task, but generation of the data is cumbersome and no standard public datasets are available. Models and algorithms created for the task are seldom compared outside the largest collaborations. 

CMB-ML datasets and libraries bridge the gap between astrophysics and machine learning. Multiple datasets are available or in-development. Code is organized into a core library, which contains the pipeline framework and associated tools, and cleaning libraries, which focus on individual cleaning methods.

Development is ongoing. Please reach out if you have questions.

## Simulation

![CMB Radiation Example](/readme_imgs/observations_and_cmb_small.png)

The real CMB signal is observed at several microwave wavelengths. To mimic this, we make a ground truth CMB map and several contaminant foregrounds. We "observe" these at the different wavelengths, where each foreground has different levels. Then we apply instrumentation effects to get a set of observed maps. The standard dataset is produced at a low resolution, so that many simulations can be used in a reasonable amount of space.

## Cleaning

Two models are included as baselines in this repository. One is a classic astrophysics algorithm, a flavor of **i**nternal **l**inear **c**ombination methods, which employs **c**osine **n**eedlets (CNILC). The other is a machine learning method (a UNet) implemented and published in the astrophysics domain, CMBNNCS. 

The CNILC method was implemented by [PyILC](https://github.com/jcolinhill/pyilc), and is described in [this paper](https://arxiv.org/abs/2307.01043).

The cmbNNCS method was implemented by [cmbNNCS](https://github.com/Guo-Jian-Wang/cmbnncs), and is described in [this paper](https://iopscience.iop.org/article/10.3847/1538-4365/ac5f4a).

The third method, the [PyTorch](https://pytorch.org/) implementation of a UNet, is very similar to cmbNNCS and many other published models. Unlike cmbNNCS, it operates on small patches of maps instead of the full sky.

## Analysis

We can compare the CMB predictions to the ground truths in order to determine how well the model works. However, because the models operate in fundamentally different ways, care is needed to ensure that they are compared in a consistent way. We first mask each prediction where the signal is often to bright to get meaningful predictions. We then remove effects of instrumentation from the predictions. The pipeline set up to run each method is then used in a slightly different way, to pull results from each method and produce output which directly compares them. The following figures were produced automatically by the pipeline, for quick review.

![Map Cleaning Example](/readme_imgs/CNILC_px_comp_sim_0005_I.png)
![Power Spectrum Example](/readme_imgs/CNILC_ps_comp_sim_0005_I.png)

Other figures are produced of summary statistics, but these are far more boring (for now!).

# Set-Up

Begin with the core CMB-ML library, available [here](https://github.com/CMB-ML/cmb-ml).

From there, the cleaning methods presented in our initial, introductory results are available in CMB-ML's adaptations of:
- [NILC repository](https://github.com/CMB-ML/cmb-ml-pyilc), powered with [PyILC](https://github.com/jcolinhill/pyilc)
- [CMBNNCS repository](https://github.com/CMB-ML/cmb-ml-cmbnncs), powered with [cmbNNCS](https://github.com/Guo-Jian-Wang/cmbnncs)

The methods above required adaptations to use original code by other researchers. For the interested practitioner, there are implementations in PyTorch which are somewhat more conventional.
- [PatchNN](https://github.com/CMB-ML/cmb-ml-patch-nn) trains on single simply-extracted patches of sky.
- [FlatSkyNN](https://github.com/CMB-ML/cmb-ml-flatsky-nn) is a reimplementation of CMBNNCS following typical conventions.


![Simulated CMB](/readme_imgs/cmb.png)
