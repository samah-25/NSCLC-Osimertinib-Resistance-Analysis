# NSCLC-Osimertinib-Resistance-Analysis
[[Galaxy](https://img.shields.io/badge/Platform-Galaxy-blue)](https://usegalaxy.org/)

> **Key Finding:** Transcriptomic profiling of Osimertinib-resistant PC9 cells reveals massive KRT17 upregulation (log2FC = 8.2), suggesting squamous transdifferentiation as a novel resistance mechanism.

End-to-end RNA-seq analysis of PC9 lung cancer cell lines under Osimertinib treatment using a reproducible Galaxy workflow.

## Project Overview
This project investigates how Osimertinib affects gene expression in NSCLC using the PC9 cell line.
I performed Differential Gene Expression Analysis on the GSE222820 dataset using a Galaxy-based RNA-seq pipeline. The aim was to identify which genes and biological pathways are activated or suppressed in response to the drug.
The results show a systematic shutdown of immune and growth-related pathways, marked by downregulation of IL7 and HLA-A, alongside strong activation of structural pathways driven by KRT17. This suggests the drug induces major transcriptomic remodeling in resistant cells.

This repository contains the full workflow from raw FASTQ to pathway-level insights, built for transparency and reproducibility.

