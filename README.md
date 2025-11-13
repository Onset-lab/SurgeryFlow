SurgeryFlow pipeline
====================
[![GitHub release (latest by date)](https://img.shields.io/github/v/release/Onset-lab/SurgeryFlow)](https://github.com/Onset-lab/SurgeryFlow/releases)
[![Nextflow](https://img.shields.io/badge/nextflow-21.10.6-brightgreen.svg)](https://www.nextflow.io/)

<img src="[https://docs.theonsetlab.com/SurgeryFlow.png" width="250">

The SurgeryFlow pipeline is a fully automated and reproducible tractography pipeline that extract requested white matter bundles.
SurgeryFlow takes raw DICOM directory (containing DWI, T1, and a reversed phase encoded b=0 if available) and the list of requested bundles.

SurgeryFlow is based on [TractoFlow](https://doi.org/10.1016/j.neuroimage.2020.116889) Pipeline.

Docker
------

Prebuilt Docker images are available here:

[https://hub.docker.com/r/onsetlab/surgeryflow](https://hub.docker.com/r/onsetlab/surgeryflow)

FOR DEVELOPERS: The containers repository is available here:
[surgeryflow-docker](https://github.com/Onset-lab/surgeryflow-docker)

Steps
-----

Diffusion processes
- preliminary DWI brain extraction (FSL)
- denoise DWI (Mrtrix3)
- gibbs correction (Mrtrix3)
- topup (FSL)
- eddy (FSL)
- extract B0 (Scilpy)
- dwi brain extraction (FSL)
- N4 DWI (ANTs)
- crop DWI (Scilpy)
- upsample DWI (Scilpy)
- upsample B0 (Scilpy)
- extract SH fitted to DWI (Scilpy)

T1 processes
- denoise T1 (Scilpy)
- N4 T1 (ANTs)
- resample T1 (Scilpy)
- T1 brain extraction (ANTs)
- crop T1 (Scilpy)
- registration on diffusion (ANTs)
- tissue segmentation (FSL)
- Lesion_On_Anat (Scilpy)

Metrics processes
- extract DTI shells (configurable in `nextflow.config`) (Scilpy)
- dti metrics (Scilpy)
- extract fODF shells (configurable in `nextflow.config`) (Scilpy)
- compute fiber response function (Scilpy)
- mean fiber response function (Scilpy)
- fODF and fODF-derived metrics (Scilpy)
- particle filter tractography maps (Scilpy)
- seeding mask (Scilpy)
- particle filter tracking (Scilpy)

White-matter bundles
- Recognize_Bundles (Scilpy)
- Clean_Bundles (Scilpy)
- Filter_Bundles (Scilpy)
- Bundles_On_Anat (Scilpy)

Nifti to DICOM
- Nifti_To_Dicom (nii2dcm)


Usage
-----

See *USAGE* or run `nextflow run main.nf --help`
