# Spatial Transcriptomics Analysis with VoltRon and Seurat

This repository contains analysis scripts from **compgen2025 Module 2: Introduction to Spatial Omics** (taught by Artur Manukyan) and demonstrates comprehensive spatial omics workflows using VoltRon and Seurat R packages. The analysis focuses on breast cancer tumor microenvironment datasets from 10x Genomics Visium and Xenium platforms.

## Features
- **Multi-modal integration**: Combines transcriptomics with H&E imaging
- **Scalable processing**: Disk-backed operations for large datasets
- **Advanced visualization**: Spatial plotting with customizable parameters
- **Comparative analysis**: Parallel processing of Visium and Xenium datasets
- **Production-ready workflows**: From raw data to biological insights

## Datasets Used
- [Xenium Human Breast Cancer Preview Dataset](https://www.10xgenomics.com/products/xenium-in-situ/preview-dataset-human-breast)
- [Visium HD CytAssist Gene Expression Dataset](https://www.10xgenomics.com/datasets/visium-hd-cytassist-gene-expression-human-breast-cancer-fresh-frozen)

-  Visium (Anterior and Sagittal Brain Sections)

  https://www.10xgenomics.com/datasets/mouse-brain-serial-section-1-sagittal-anterior-1-standard-1-1-0
  
  https://www.10xgenomics.com/datasets/mouse-brain-serial-section-1-sagittal-posterior-1-standard-1-1-0

- scRNASeq (Allen Institute adult mouse brain cortical cells)

  https://www.nature.com/articles/nn.4216

  https://www.dropbox.com/s/cuowvm4vrf65pvq/allen_cortex.rds?dl=1

- Xenium In Situ Replicate 1 (Breast Cancer)

  https://www.10xgenomics.com/products/xenium-in-situ/preview-dataset-human-breast

- Xenium Lung COVID19

  https://bimsbstatic.mdc-berlin.de/landthaler/VoltRon/Multiomics/acutecase1_annotated.rds

- Visium Cytassist (Breast Cancer)

  https://www.10xgenomics.com/products/xenium-in-situ/preview-dataset-human-breast


## Computational Environment
- **R 4.4.2**
- Executed in **rolv.io** compute R sessions
- Memory configuration: `options(java.parameters = "-Xmx8g")`

## Installation Requirements

### Core Dependencies
```r
install.packages("Seurat")
BiocManager::install("rhdf5")
BiocManager::install("ComplexHeatmap")
devtools::install_github("dmcable/spacexr")
```
### VoltRon Dependencies
```r
# Note: RBioFormats may require Java troubleshooting
BiocManager::install("RBioFormats")  
BiocManager::install(c("HDF5Array", "basilisk"))

devtools::install_github(c(
  "BIMSBbioinfo/HDF5DataFrame",
  "BIMSBbioinfo/ImageArray",
  "bnprks/BPCells/r@v0.3.0",  # Must install before VoltRon
  "vitessce/vitessceR",
  "immunogenomics/presto"
))
install.packages("ggnewscale")
```

### **Installation Notes**

Refer to VoltRon's dependency guide for troubleshooting

RBioFormats may require manual Java configuration

Install BPCells v0.3.0 before VoltRon


## Analysis Workflow

### Visium Data Analysis

**1. Data Import**

Load 10x Genomics Visium data

Process sample metadata and feature information

Visualize H&E and fluorescence channels

**2. Transcriptomics Processing**

Normalization and feature selection (top 3000 variable genes)

Dimensionality reduction (PCA, UMAP)

Graph-based clustering (SNN)

**3. Integration with Seurat**

Comparative analysis using Seurat's spatial functions

Marker gene identification and visualization

Spatial localization of clusters

**4. Spatial Deconvolution**

Cell type proportion estimation

Niche clustering and visualization

Composition heatmaps


### Xenium Data Analysis

**1. Data Processing**

Quality filtering (minimum 5 transcripts/cell)

Efficient HDF5 storage for large datasets

Memory-optimized operations

**2. Single-cell Analysis**

Normalization and dimensionality reduction

Cell clustering and annotation

Marker gene analysis

**3. Advanced Spatial Analysis**

Niche clustering (radius-based neighborhoods)

Hotspot analysis for spatial patterns

Multi-assay registration (Visium + Xenium)

## Outputs
**1. Quality Control:**

Visium Spots
Visium spot alignment with H&E histology

**2. Clustering:**

UMAP Clusters
UMAP visualization of clusters

**3. Spatial Features:**

Cell Type Spatial
Cell-type specific spatial patterns

**4. Advanced Analysis:**

Hotspots
Hotspot analysis of PGR expression

## Running the Analysis
Clone this repository

Install all dependencies (see above)

Update file paths in the script to match your local data directories

Run sections sequentially:
```r
source("spatial_omics_analysis.R")
```

### Expected Runtime

Visium Processing	~30 minutes	16GB

Xenium Processing	~45 minutes	32GB

Full Integration	~1 hour	32GB+


## References

VoltRon GitHub: https://github.com/BIMSBbioinfo/VoltRon

Seurat Spatial Tutorials: https://satijalab.org/seurat/articles/spatial_vignette.html

10x Genomics Spatial Analysis: https://www.10xgenomics.com/spatial-transcriptomics
