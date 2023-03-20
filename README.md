# Papet predictive models

---------------------------------------------

This repository contains models to predict 5-methyl cytosine (5mC) from PacBio SequelII sequencing data.

These models were trained using PAcbio Prediction of Epigenetics Technology (Papet) `model-kinetic` software ([see documentation](https://github.com/ngs-ai-org/papet#model-kinetic)) for more informations. These models can be used to predict 5mC using Papet `predict` software ([see documentation](https://github.com/ngs-ai-org/papet#predict))

## Table of content

1. [Content](#content)
2. [About kinetic models](#about-kinetic-models)
3. [About the training](#about-the-training)
4. [Usage](#usage)


## Content

Six different types of models are present in this repository:
- models of the raw kinetics, stored in the `raw` directory 
- models of the normalized kinetics, stored in `normalized`
- models of the raw kinetics accounting for neighbouring position dependencies, stored in the `diposition` directory
- models of the normalized kinetics accounting for neighbouring position dependencies, stored in the `diposition_normalized` directory
- models of the raw kinetics accounting for all possible pairwise position dependencies, stored in the `pairwise` directory
- models of the normalized kinetics accounting for all possible pairwise position dependencies, stored in the `pairwise_normalized` directory


## About kinetic models

To learn more about PacBio kinetics and the kinetic models we devised, see the [dedicated documention](https://github.com/ngs-ai-org/ngsaipp/blob/master/PacBio_kinetics.md#kinetic-models).

## About the training

The models were trained using two SequelII whole genome sequencing datasets produced by PacBio, originating from hg002.

The first dataset was created by subjecting a hg002 DNA sample to whole genome amplification (WGA). The resulting DNA was used to create a library deprived of epigenetic modifications. Eventually, the library was sequenced using a SequelII sequencer. 

The second dataset was created by subjecting a fraction of the 1st sample to a Sssl enzymatic treatment. The Sssl enzyme deposites 5mC to CpG specifically, leading to the creation of CpG methylated library. This library was sequencingd using a SequelII sequencer. 

The resulting CCSs were mapped against hg38p8 genome reference. 

The kinetic sequence normalization model was trained on the WGA dataset using [papet `model-sequence`](https://github.com/ngs-ai-org/papet#model-sequence) using 11-mers. All the kinetic signal models were then trained using a 17bp window, centered on each individual CpGs using [papet `model-kinetic`](https://github.com/ngs-ai-org/papet#model-kinetic).

The unmethylated CpG kinetic models were trained on the WGA dataset. The methylated CpG kinetic models were trained on the Sssl dataset. 


## Usage

The models need to be decompressed prior usage. Then, simply use them with [papet `predict`](https://github.com/ngs-ai-org/papet#predict) with the `--modelMeth` and `--modelUnmeth` options.

Note that the file extensions (`.rawkineticmodel`, `.normalizedkineticmodel`, etc) must not be altered.


## Authors

* **Romain Groux**