---
title: 'Fetpype: An Open-Source Pipeline for Reproducible Fetal Brain MRI Analysis'
tags:
  - Python
  - fetal brain MRI
  - super-resolution reconstruction
  - segmentation
  - surface extraction
authors:
  - name: Thomas Sanchez
    orcid: 0000-0003-3668-5155
    equal-contrib: true
    affiliation: "1, 2" # (Multiple affiliations must be quoted)
    corredponsing: true
  - name: Gerard Martí-Juan
    orcid: 0000-0003-4729-7182
    equal-contrib: true
    affiliation: 3 # (Multiple affiliations must be quoted)
  - name: David Meunier
    orcid: 0000-0002-5812-6138
    affiliation: 4
  - name: Gemma Piella
    orcid: 0000-0001-5236-5819
    affiliation: 3
  - name: Meritxell Bach Cuadra
    orcid: 0000-0003-2730-4285
    affiliation: "1, 2"
  - name: Guillaume Auzias
    orcid: 0000-0002-0414-5691
    affiliation: 4
affiliations:
 - name: CIBM – Center for Biomedical Imaging, Switzerland
   index: 1
 - name: Department of Diagnostic and Interventional Radiology, Lausanne University Hospital and University of Lausanne, Switzerland
   index: 2
 - name: BCN MedTech, Department of Engineering, Universitat Pompeu Fabra, Spain
   index: 3
 - name: Aix-Marseille Université, CNRS, Institut de Neurosciences de La Timone, France
   index: 4
date: 19 June 2025
bibliography: paper.bib
---

# Summary

Fetal brain Magnetic Resonance Imaging (MRI) is instrumental for assessing neurodevelopment *in utero*. 
However, analyzing this data presents significant challenges due to fetal motion during the acquisition, 
and constraints on scan duration inducing low signal-to-noise ratio.
Complex and specific image processing pipelines are required, involving multiple steps, including motion correction, super-resolution reconstruction, tissue segmentation, and extraction of measures. 
Various specialized tools exist for individual steps, but open-source, user-friendly workflows that go from raw image to volume and surface analysis are missing.
This lack of standardization hinders reproducibility across studies and limits the adoption 
of advanced analysis techniques for researchers and clinicians. 
We introduce `Fetpype`, an open-source Python library designed to streamline 
and standardize the preprocessing and analysis of fetal brain MRI data.


# Statement of need

'Fetpype' is a Python package integrating several state-of-the-art established neuroimaging software principles and tools into an open-source, robust, reproducible, and extensible framework.
This is achieved by implementing the following five core building blocks: 


1. **Data Standardization**: `Fetpype` expects input data organized according to the Brain Imaging Data Structure (BIDS) standard [@gorgolewski2016brain], promoting interoperability and simplifying data management. 
2. **Containerization**: Individual processing tools are encapsulated within Docker or Singularity containers. This ensures reproducibility and reduces installation issues, providing a better experience for the end user. In addition, this principle makes future extensions of 'Fetpype' with additional processing steps or features by us or other contributors straightforward. 
3. **Workflow Management**: The processing workflows are based on the `Nipype` library [@gorgolewski2011nipype] that provides a robust interface for combining different processing steps from different containers or packages, facilitating data caching and parallelization.
The workflows are designed by combining modular processing nodes enforcing the versatility and allowing pipelines to be easily recombined, adapted, or improved. 
4. **Configuration**: Pipeline configuration is managed using simple YAML files and the Hydra library [@Yadan2019Hydra].
Users can easily select between different modules or parameters without directly modifying the code. 
The current implementation of Fetpype integrates modules for **data preprocessing**, **super-resolution reconstruction** (NeSVoR [@xu2023nesvor], SVRTK [@kuklisova-murgasova_reconstruction_2012; @uus2022automated], or NiftyMIC [@ebner2020automated]), **segmentation** (BOUNTI [@uus2023bounti] or the developing human connectome project pipeline [@makropoulos2018developing]) and **cortical surface extraction** (using a custom implementation available at https://github.com/fetpype/surface_processing based on [@bazin2005topology; @bazin2007topology; @ma2022cortexode]).
All these modules are based on docker or singularity containers released by their authors, ensuring reproducible results aligned with corresponding publications.
5. **Documentation**: We provide an extensive and detailed documentation website inline with the code.
The intention is to guide users along the classical installation and running steps, but also to document each processing module and corresponding parameters.
This allows for the fast appropriation of the building blocks of the proposed workflows, such that tuned or improved workflows can be implemented, tested and shared with minimal efforts.

`Fetpype` was designed to be used by the fetal MRI community by providing a standardized, reproducible and flexible open-source platform for preprocessing and analysis. We believe this tool can facilitate research, improve comparability between studies, and foster collaboration. The pipeline is publicly available on GitHub (https://github.com/fetpype/fetpype), and its open-source nature and modular design facilitate community involvement: researchers can integrate their own tools by creating corresponding `Nipype` interfaces and container wrappers, following the package contribution guidelines.

In the future, we plan to supplement `Fetpype` with an automated reporting library containing automated quality control [@sanchez2024fetmrqc; @sanchez2025automatic], subject-wise and population-wise biometry and volumetry [@esteban2017mriqc], as well as spectral analysis [@germanaud2012larger]. We welcome contributions of authors desiring to integrate their method to `Fetpype`. 

![The different steps covered by `Fetpype`. The current version of `Fetpype` implements the different processing steps needed to compute clinically relevant measures like biometric, volumetric or surface descriptors, but does not implement them. \label{fig:fetpype}](fetpype.png)

# Acknowledgements
This work was funded by Era-net NEURON MULTIFACT project (TS: Swiss National Science Foundation grants 31NE30_203977, 215641; GA: French National Research Agency, Grant ANR-21-NEU2-0005; GMJ, GP:  Ministry of Science, Innovation and Universities: MCIN/AEI/10.13039/501100011033/), and the SulcalGRIDS Project, (GA: French National Research Agency Grant ANR-19-CE45-0014).  We acknowledge the CIBM Center for Biomedical Imaging, a Swiss research center of excellence founded and supported by CHUV, UNIL, EPFL, UNIGE and HUG. This research was also supported by grants from NVIDIA and utilized NVIDIA RTX6000 ADA GPUs.


# References
