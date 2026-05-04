# NSCLC-Osimertinib-Resistance-Analysis
[[Galaxy](https://img.shields.io/badge/Platform-Galaxy-blue)](https://usegalaxy.org/)

Complete RNA-seq pipeline from raw FASTQ to biological interpretation of Osimertinib resistance in PC9 lung cancer cells.

> **Key Finding:** Transcriptomic profiling of Osimertinib-resistant PC9 cells reveals a dual escape strategy: (1) Immune evasion via systematic shutdown of immune genes IL7 and HLA-A, and (2) Squamous transdifferentiation via strong KRT17 upregulation (log2FC = 3.93). Together, these suggest the cells remodel their identity to evade both therapy and immune detection.

## Project Overview
This project investigates how Osimertinib affects gene expression in NSCLC using the PC9 cell line.
I performed Differential Gene Expression Analysis on the GSE222820 dataset using a Galaxy-based RNA-seq pipeline. The aim was to identify which genes and biological pathways are activated or suppressed in response to the drug.
The results show a systematic shutdown of immune and growth-related pathways, marked by downregulation of IL7 and HLA-A, alongside strong activation of structural pathways driven by KRT17. This suggests the drug induces major transcriptomic remodeling in resistant cells.

This repository contains the full workflow from raw FASTQ to pathway-level insights, built for transparency and reproducibility.

## Repository Structure
```
📁 NSCLC-Osimertinib-Resistance-Analysis/
├── 📁 1_data/
│   ├── counts_matrix.csv          # Raw gene counts from featureCounts
│   ├── DGE_results_limma.csv      # Full differential expression table
│   └── metadata.csv               # Sample info: control vs resistant
├── 📁 2_workflow/
│   └── galaxy-workflow.ga         # Import this to Galaxy to reproduce
├── 📁 3_results/
│   ├── volcano_plot.png           # Main DGE visualization
│   ├── pathway_enrichment.png     # g:Profiler results
│   └── KRT17_boxplot.png          # Expression of key gene
└── README.md                      # You are here
```
## Analytical Workflow (Galaxy Pipeline)
The full reproducible workflow is available in `2_workflow/galaxy-workflow.ga`. Import it into Galaxy to reproduce the entire analysis.

1. **Raw Data Processing**: Downloaded SRA data for GSE222820 and assessed read quality with FastQC
2. **Preprocessing**: Removed adapters and low-quality reads using Trimmomatic
3. **Alignment**: Aligned reads to the human reference genome (hg38) using HISAT2
4. **Quantification**: Generated gene-level count matrix from aligned reads using featureCounts
5. **Differential Expression**: Identified significantly dysregulated genes between conditions using limma-voom
6. **Pathway Analysis**: Performed GO and KEGG pathway enrichment on significant genes using Enrichr to interpret biological meaning
