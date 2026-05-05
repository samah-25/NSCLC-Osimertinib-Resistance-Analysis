
# 2_workflow: Galaxy Analysis Pipeline

This folder contains the Galaxy workflow used to generate the results in `1_data/` from raw FASTQ files.

## Files

| File | Description |
| --- | --- |
| `Workflow.ga` | Galaxy workflow file. Contains all analysis steps from SRA download to limma-voom |
| `environment.yml` | List of tool versions used by Galaxy. For reference and reproducibility |

## How to reproduce this analysis in Galaxy

1. Go to https://usegalaxy.org and log in
2. `Workflow` → `Import` → Upload `Workflow.ga`
3. `Upload Data` → Upload `1_data/0_SRR_Acc_List.txt` from this repository
4. `Workflow` → `Run Workflow` → Select the uploaded SRR list as input
5. Click `Run Workflow` and wait for all 8 steps to finish

**Final outputs will match the files in `1_data/`:**
- Raw counts matrix
- limma-voom DGE results table

## Tools & Versions Used
- **Data Download:** SRA-Tools v3.0.5
- **Quality Control:** FastQC v0.12.1  
- **Alignment:** HISAT2 v2.2.1 to
