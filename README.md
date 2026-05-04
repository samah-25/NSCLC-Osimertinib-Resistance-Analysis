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

## Key Results Summary

### 1. Differential Expression Summary
Using stringent filters (|logFC| ≥ 3, adj.P < 0.05), we identified **279 high-confidence DEGs**:
- **221 Up-regulated genes** in resistant PC9-OR cells
- **58 Down-regulated genes** in resistant PC9-OR cells

### 2. Top Driver Genes
**Most Down-regulated:** WNT5A (-9.12), ALDH1A1 (-7.79), IL7 (-3.67)  
**Most Up-regulated:** THBD (+5.78), S100A7 (+4.63), KRT17 (+3.93), HLA-A (+3.49)

### 3. Biological Interpretation: Dual-Escape Model
**Mechanism 1: Lineage Plasticity**  
Loss of lung markers `WNT5A`, `MIR200B` and gain of squamous markers `KRT17`, `S100A7` indicates a switch to a drug-insensitive state. Supported by GO term "Cornified Envelope Formation" (P=0.003).

**Mechanism 2: Inflammatory Reprogramming**  
Upregulation of `THBD`, `CASP1`, `HLA-A/B` with loss of T-cell cytokines `IL7`, `IL4` suggests a pro-inflammatory niche that impairs immune clearance. Supported by KEGG term "Antigen Processing and Presentation" (Combined Score=93.86).

**Conclusion:** Resistance is driven by combined loss of epithelial identity and gain of an inflammatory, squamous-like state. This model matches findings from Shi et al. 2025 [PMID: 40796706].

## Data Availability

- **Raw RNA-seq Data:** NCBI Gene Expression Omnibus (GEO) under accession number [GSE222820](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE222820)
- **Processed Data:** All intermediate and final processed files (counts, DEG lists, enrichment results) are available in the `1_data/` and `results/tables/` directories of this repository.
- **Analysis Workflow:** The complete Galaxy workflow is available in `2_workflow/galaxy-workflow.ga`.

  
