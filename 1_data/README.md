# 1_data: Raw Input Files for GSE222820 Analysis

This folder contains all input files required to reproduce the differential expression analysis starting from raw sequencing data.

## 1. Data Source & Experimental Design

- **GEO Accession:** [GSE222820](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE222820)
- **SRA Project:** [SRP411229](https://trace.ncbi.nlm.nih.gov/Traces/?view=study&acc=SRP411229) ← contains all raw FASTQ files for this study
- **Cell Line:** PC9 NSCLC
- **Experimental Groups:** 6 samples total
    1. **PC9_Sensitive (n=3):** Osimertinib-naive parental cell line
    2. **PC9_OR (n=3):** Osimertinib-Resistant cell line derived after chronic drug exposure

**Note:** Specific SRR run accessions for all 6 samples are listed in `0_SRR_Acc_List.txt` and annotated in `3_sample_metadata.csv`. Raw FASTQ files are not stored in this repo due to size.

## 2. File Inventory

| Filename | Description | Dimensions | How it was generated |
| :--- | :--- | :---: | :--- |
| `0_SRR_Acc_List.txt` | List of 6 SRA run accessions for batch download. Use with `prefetch` or `fastq-dump`. | 6 lines | Curated from GEO GSE222820 |
| `1_raw_counts_matrix.csv` | Raw gene-level read counts. First column = Ensembl Gene ID, columns 2-7 = counts for samples in the same order as `0_SRR_Acc_List.txt`. | 57247 genes x 7 columns | `featureCounts v2.0.3` on HISAT2-aligned BAMs. Params: `-t exon -g gene_id` |
| `2_DGE_results_limma_voom.csv` | Complete `limma-voom` output for all 15,913 tested genes. | 15913 genes x 8 columns | `limma-voom v3.54.0` using files `1` + `3` from this folder |
| `3_sample_metadata.csv` | Design file mapping each SRR accession to its `Condition`. Defines the `Sensitive vs OR` comparison. | 6 samples x 3 columns | Manual curation from GEO sample metadata |

## 3. Reproduction Order
1. Download FASTQs: `cat 0_SRR_Acc_List.txt | xargs prefetch`
2. Check experimental design: `3_sample_metadata.csv`
3. Run DGE: `1_raw_counts_matrix.csv` → `limma-voom` → `2_DGE_results_limma_voom.csv`
