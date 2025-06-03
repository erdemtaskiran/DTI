# DTI Preprocessing Pipeline for Multimodal Data Fusion Analysis

This repository contains a comprehensive UNIX shell script for automated Diffusion Tensor Imaging (DTI) preprocessing using FSL (FMRIB Software Library) tools. The pipeline is specifically designed to prepare high-quality Fractional Anisotropy (FA) images for **multimodal data fusion and unsupervised learning analysis** using the **Fusion ICA Toolbox (FIT)**. 

## Purpose

This preprocessing pipeline generates standardized, analysis-ready FA images optimized for advanced multimodal neuroimaging analyses including:

- **tIVA** (transposed Independent Vector Analysis)
- **mCCA+jICA** (multiset Canonical Correlation Analysis + joint Independent Component Analysis)
- **Parallel ICA** (PICA)
- Other multimodal fusion techniques available in the FIT toolbox

## Pipeline Overview

The automated preprocessing script performs the following key steps to ensure FA images meet the quality standards required for multimodal fusion analysis:

### 1. Data Preparation & Quality Control
- Extracts b0 volumes from main DWI and reverse phase-encoding acquisitions
- Prepares data for distortion correction protocols

### 2. Advanced Distortion Correction
- **TOPUP**: Corrects susceptibility-induced distortions using opposite phase-encoding directions
- Essential for maintaining spatial accuracy required in multimodal registration

### 3. Brain Extraction & Masking
- **BET**: Performs optimized skull stripping (f=0.25) for DTI data
- Creates precise brain masks critical for accurate tensor fitting

### 4. Motion & Artifact Correction
- **EDDY**: Comprehensive correction for:
  - Head motion between volumes
  - Eddy current distortions
  - Residual susceptibility artifacts
- Ensures data quality suitable for sensitive ICA decompositions

### 5. DTI Model Fitting
- **DTIFIT**: Generates high-quality FA maps from corrected diffusion data
- Produces the primary input for multimodal fusion analyses

### 6. Spatial Standardization for Group Analysis
- **FLIRT + FNIRT**: Two-stage registration to MNI152 standard space
- Ensures spatial correspondence across subjects for group-level fusion
- Critical for valid cross-subject component analysis in tIVA and Parallel ICA

### 7. Optimization for FIT Toolbox
- **Spatial smoothing** (3.4mm = 8FWHM): Improves signal-to-noise ratio for ICA decomposition
- **Standardized output format**: Compatible with FIT toolbox input requirements
- **Quality-controlled FA maps**: Ready for integration with other modalities (fMRI, sMRI, etc.)

## Multimodal Integration Ready

The final FA images (`*_FA_final.nii.gz`) are specifically prepared for:

- **Cross-modal correspondence**: Spatially aligned for fusion with fMRI, structural MRI, or other modalities
- **Group-level ICA**: Normalized and smoothed for stable component decomposition in Parallel ICA
- **tIVA analysis**: Optimized data quality for transposed Independent Vector Analysis across multiple datasets
- **FIT toolbox compatibility**: Formatted and processed according to toolbox requirements
- **Statistical robustness**: High-quality preprocessing reduces noise that could confound multimodal analyses

## Requirements

- FSL (FMRIB Software Library)
- FIT (Fusion ICA Toolbox) for downstream analysis
- Standard DTI acquisition with reverse phase-encoding for distortion correction



