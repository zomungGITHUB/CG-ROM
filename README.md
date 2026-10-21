# Companion code and data for the work "Sequential Calibration of Soil Parameters Using a Two-Step Surrogate for High-Dimensional Geotechnical Outputs"

  This repository contains the MATLAB based implementation of the PCA-PCE reduced order modelling for geotechnical correlated high-dimensional outputs and uncertainty quantification. 
  ![alt text](image.png)
  Please cite this work, in case you use and/or refer to the PCA-PCE UQ and sequential Bayesian calibration worke.

 --------------------
# Table of Contents
<!-- TOC depthFrom:2 depthTo:4 withLinks:1 updateOnSave:1 orderedList:0 -->
- [Overview](#Overview)
- [Real-world application and deployment](#real-world-application-and-deployment)
- [System Requirements](#Requirements)
- [Instructions](#Instructions)
- [Contact](#Contact)
<!-- /TOC -->
---------------------
# Overview <a name="Overview"></a>
This code is a companion to an academic research paper. If you use this work in an academic context, please cite the following publication(s):

  @article{yang2024two,
    title={A two-step surrogate method for sequential uncertainty quantification in high-dimensional inverse problems},
    author={Yang, Ningxin and Le, Truong and Potts, David M and others},
    journal={arXiv preprint arXiv:2407.11600},
    year={2024}
  }

**Keywords:** Sequential Bayesian inversion; Soil parameters; Surrogate modelling; Dimensionality reduction; High dimensions

This folder contains code and data to reproduce the results in the associated paper. In particular, the provided scripts will reproduce all graphs related to Table 3 and global sensitivity analysis, as well as the posterior uncertainty analyses reported in the study.

Open main.mlx file using MATLAB
## step 1
change your working path to `...\SBI\RUN`;

add your UQlab package core path `...\UQlab\UQLab_Rel2.0.0\UQLab_Rel2.0.0\core`;

add your subroutine code path `...\SBI\Main\subroutines`;

Run Matlab;

## step 2
Cases A, B, C and D refers to the usage of DR and the number of training numbers. 

Here, we can just control the two switch to change the number FE run traing and DR:`AnParam.DR` and `AnParam.TrainDataPerc` to reproduce the results.

 e.g., `AnParam.TrainDataPerc = 1` (means FE training run number = 138)

  `AnParam.TrainDataPerc = 0.1-1.0;`
  `AnParam.DR = "on/off;`

## step 3
click run

---------------------
# Real-world application and deployment <a name="real-world-application-and-deployment"></a>
This repository is best understood as a research-grade computational workflow for uncertainty quantification and inverse calibration, rather than as a finished commercial software product. It provides a sound basis for practical deployment in geotechnical engineering and scientific decision support.

## Architecture overview
```text
┌──────────────────────────────────────────────────────────────────────────────┐
│                     Scientific Problem Definition                             │
│  Sequential Bayesian calibration of soil parameters and geotechnical outputs │
└───────────────────────────────┬──────────────────────────────────────────────┘
                                │
                                ▼
┌──────────────────────────────────────────────────────────────────────────────┐
│                             Data Acquisition Layer                             │
│  - field/lab/numerical data                                                  │
│  - model inputs and target outputs                                            │
│  - stored under: RUN/data/input                                              │
└───────────────────────────────┬──────────────────────────────────────────────┘
                                │
                                ▼
┌──────────────────────────────────────────────────────────────────────────────┐
│                         Configuration and Experiment Setup                    │
│  - RUN/data/config.yaml                                                      │
│  - DR on/off                                                                 │
│  - TrainDataPerc                                                             │
│  - FE training run settings                                                  │
│  - calibration settings                                                     │
└───────────────────────────────┬──────────────────────────────────────────────┘
                                │
                                ▼
┌──────────────────────────────────────────────────────────────────────────────┐
│                         MATLAB Computational Core                              │
│  Main/main.mlx                                                              │
│  Entry point for model execution                                             │
│                                                                              │
│  Core routine flow:                                                         │
│  - data loading                                                             │
│  - dimensionality reduction                                                 │
│  - surrogate construction                                                    │
│  - Bayesian calibration / inverse analysis                                   │
│  - uncertainty quantification                                                │
└───────────────────────────────┬──────────────────────────────────────────────┘
                                │
                                ▼
┌──────────────────────────────────────────────────────────────────────────────┐
│                        Subroutine and Algorithm Layer                           │
│  Main/subroutines                                                           │
│  - PCA / reduced-order modeling                                              │
│  - surrogate construction                                                    │
│  - likelihood and posterior evaluation                                      │
│  - MCMC / sequential update                                                  │
│  - plotting and post-processing                                              │
└───────────────────────────────┬──────────────────────────────────────────────┘
                                │
                                ▼
┌──────────────────────────────────────────────────────────────────────────────┐
│                           Validation and Diagnostics                          │
│  - convergence checks                                                        │
│  - physical plausibility                                                    │
│  - accuracy against benchmark                                                │
│  - uncertainty propagation                                                  │
│  - residual and sensitivity diagnostics                                     │
└───────────────────────────────┬──────────────────────────────────────────────┘
                                │
                                ▼
┌──────────────────────────────────────────────────────────────────────────────┐
│                           Output and Reporting Layer                          │
│  RUN/data/output                                                            │
│  - figures                                                                   │
│  - posterior summaries                                                      │
│  - parameter uncertainty                                                    │
│  - analysis results                                                          │
└───────────────────────────────┬──────────────────────────────────────────────┘
                                │
                                ▼
┌──────────────────────────────────────────────────────────────────────────────┐
│                    Engineering Decision Support and Deployment                │
│                                                                              │
│  ┌──────────────────────┐    ┌──────────────────────┐                     │
│  │ MATLAB App / GUI      │    │ Standalone Tool      │                     │
│  │ Desktop for users     │    │ MATLAB Compiler      │                     │
│  └──────────────────────┘    └──────────────────────┘                     │
│              │                             │                                  │
│              └───────────────┬─────────────┘                                  │
│                              │                                                │
│                     ┌──────────────────────┐                                 │
│                     │ API / Python Wrapper │                                 │
│                     │ Integration          │                                 │
│                     └──────────────────────┘                                 │
│                              │                                                │
│                              ▼                                                │
│                    Real-world engineering use                                 │
│                    - parameter calibration                                      │
│                    - uncertainty-informed decisions                              │
│                    - research-to-practice translation                             │
└──────────────────────────────────────────────────────────────────────────────┘
```

## Recommended deployment model for MATLAB research code
The most practical deployment path for this repository is:

1. Keep the MATLAB code as the validated scientific engine.
2. Separate the algorithm from the interface using structured input and output schemas.
3. Use configuration files for experiment settings and model parameters.
4. Package the workflow as either:
   - a MATLAB desktop app,
   - a compiled standalone tool,
   - a REST API or Python wrapper for broader integration,
   - or a batch execution system for repeated engineering use.
5. Add validation, logging, reproducibility checks, and standard output reports.
6. Pilot the method on real geotechnical data before broader deployment.

This enables the repository to evolve from a paper companion into a usable decision-support tool for engineering applications.

## Roadmap from paper to production
The repository can mature through a staged pathway:

- Phase 1: Reproduce the paper results reliably in MATLAB.
- Phase 2: Modularize the workflow into reusable functions and clear interfaces.
- Phase 3: Standardize configuration and data handling.
- Phase 4: Benchmark accuracy, computational cost, and convergence.
- Phase 5: Package the method for end-user access.
- Phase 6: Pilot deployment with real datasets and engineering validation.
- Phase 7: Operational deployment with logging, monitoring, and retraining workflows.

## Practical real-world application flow
```text
Research problem / geotechnical inverse problem
        ↓
Define uncertain parameters and objectives
        ↓
Collect field, lab, or numerical data
        ↓
Prepare input data in RUN/data/input
        ↓
Set experiment parameters in RUN/data/config.yaml
        ↓
Open Main/main.mlx in MATLAB
        ↓
Load routines from Main/subroutines
        ↓
Run dimensionality reduction + surrogate modeling
        ↓
Run sequential Bayesian calibration / uncertainty quantification
        ↓
Generate outputs in RUN/data/output
        ↓
Validate convergence and physical plausibility
        ↓
Tune settings (DR, TrainDataPerc, FE training runs)
        ↓
Refine and repeat
        ↓
Package as a reusable tool or service
        ↓
Deploy for engineering use and decision support
```

This repository is best seen as a scientific engine for uncertainty-aware calibration and inverse analysis, with clear potential to become an applied engineering tool for soil parameter estimation and reliability-informed decision making.

---------------------
# Requirements <a name="Requirements"></a>
The following functions used in the scripts require toolboxes to be installed:
1. UQLab packages for MCMC https://www.uqlab.com/
2. Matlab 2024 (HPC also supported)
3. Statistics and Machine learning toolbox;Optimization toolbox;Global Optimization toolbox


---------------------
## Contact <a name="Contact"></a>
Thank you very much for your interest in our work， it's a pleasure to connect with you here. We are committed to open-source code and transparent, reproducible scientific research. All the data and code are available to support replication and extension of the work.

Ningxin Yang

n.yang23@imperial.ac.uk
