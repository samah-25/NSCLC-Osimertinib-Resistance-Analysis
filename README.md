# NSCLC-Osimertinib-Resistance-Analysis
[[Galaxy](https://img.shields.io/badge/Platform-Galaxy-blue)](https://usegalaxy.org/)

Complete RNA-seq pipeline from raw FASTQ to biological interpretation of Osimertinib resistance in PC9 lung cancer cells.

> **Key Finding:** 
Analysis of GSE222820 identified **279 high-confidence differentially expressed genes** `(|log2FC| ≥ 3, adj.P < 0.05)` supporting a dual-axis model of resistance:

1.  **Lineage Plasticity:** Coordinated loss of lung adenocarcinoma identity markers `WNT5A` (-9.12 log2FC) with concurrent gain of squamous differentiation markers `KRT17` (+3.93), consistent with adenocarcinoma-to-squamous transdifferentiation.

2.  **Immune Microenvironment Reprogramming:** Establishment of a pro-inflammatory state via `THBD` (+5.78) and `CASP1` (+4.60) upregulation, combined with loss of T-cell homeostatic signals `IL7` (-3.67). This is accompanied by a paradoxical upregulation of MHC-I components such as HLA-A (+3.49), suggesting altered antigen presentation despite T-cell suppression.

3.  **Potential Clinical Relevance:** Downregulation of the "Dilated Cardiomyopathy" pathway, providing a transcriptomic signature that aligns with the known cardiac adverse events associated with Osimertinib.
This model independently validates the KRT-driven immune dysfunction mechanism reported by Shi et al. 2025 [[PMID: 40796706](https://pubmed.ncbi.nlm.nih.gov/40796706/)] and extends it by linking resistance to a cardiotoxicity signature.

## Project Overview
This project investigates how Osimertinib affects gene expression in NSCLC using the PC9 cell line.
I performed Differential Gene Expression Analysis on the GSE222820 dataset using a Galaxy-based RNA-seq pipeline. The aim was to identify which genes and biological pathways are activated or suppressed in response to the drug.
The results show a systematic shutdown of immune and growth-related pathways, marked by downregulation of IL7 alongside significant upregulation of HLA-A, alongside strong activation of structural pathways driven by KRT17. This suggests the drug induces major transcriptomic remodeling in resistant cells.

This repository contains the full workflow from raw FASTQ to pathway-level insights, built for transparency and reproducibility.

## Repository Structure
```
📁 NSCLC-Osimertinib-Resistance-Analysis/
├── 📁 1_data/
│   ├── counts_matrix.csv          # Raw gene counts from featureCounts
│   └── metadata.csv               # Sample info: control vs resistant
├── 📁 2_workflow/
│   └── galaxy-workflow.ga         # Import this to Galaxy to reproduce
├── 📁 3_results/
|   ├── DGE_results_limma_voom.csv
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
supporting a dual-escape model of resistance.

| Mechanism | Key Genes | Log2FC | Evidence & Interpretation |
| :--- | :--- | :---: | :--- |
| **1. Lineage Plasticity** <br> *Adeno-to-Squamous Switch* | `WNT5A` | **-9.12** | Loss of master lung identity regulator. GO: "Cornified Envelope Formation" (P=0.003). |
| | `KRT17` | **+3.93** | Gain of squamous differentiation marker. Validates KRT-driven resistance model [PMID: 40796706]. |
| **2. Immune Reprogramming** <br> *T-cell Dysfunction* | `IL7` | **-3.67** | Loss of critical T-cell survival cytokine, consistent with reduced CD8+ T-cell activity. |
| | `HLA-A` | **+3.49** | Paradoxical MHC-I upregulation. KEGG: "Antigen Processing and Presentation" (Score=93.86). |
| | `THBD` | **+5.78** | Top upregulated gene. Induces pro-inflammatory, pro-coagulant tumor microenvironment. |
| **3. 3. Potential Clinical Relevance** <br> *Cardiotoxicity Signature* | `Dilated Cardiomyopathy` Pathway | **↓ Down** | Transcriptomic signature aligns with known cardiac adverse events of Osimertinib. |
The full differential expression results are available in 3_results/DGE_results_limma_voom.csv.

## Independent Validation of Published Mechanisms

This work supports the KRT-driven immune dysfunction model of osimertinib resistance reported by Shi et al. 2025 (Discov Oncol, PMID: 40796706)(https://pubmed.ncbi.nlm.nih.gov/40796706/), confirming the role of KRT-family genes and T-cell suppression in osimertinib resistance. 
The analysis further extends these findings by identifying a transcriptomic signature consistent with cardiotoxicity, providing a potential mechanistic link between the resistance phenotype and clinical adverse events.

**Conclusion:** 
This work supports the KRT-driven immune dysfunction model of osimertinib resistance and suggests a potential mechanistic link to its clinical cardiotoxicity profile.


## Data Availability

- **Raw RNA-seq Data:** NCBI Gene Expression Omnibus (GEO) under accession number [GSE222820](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE222820)
- **Processed Data:** All intermediate and final processed files (counts, DEG lists, enrichment results) are available in the `1_data/` and `3_results/` directories of this repository.
- **Analysis Workflow:** The complete Galaxy workflow is available in `2_workflow/galaxy-workflow.ga`.

  
