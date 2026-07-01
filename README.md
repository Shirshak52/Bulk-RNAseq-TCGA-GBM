---
editor_options: 
  markdown: 
    wrap: none
---

# **Bulk RNA-seq TCGA-GBM Downstream Analysis: Proneural vs Mesenchymal GBM Subtypes**

[![R 4.5.3](https://img.shields.io/badge/R-4.5.3-276DC3.svg)](https://www.r-project.org/) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**End-to-end bulk RNA-seq downstream analysis pipeline** applied to the **TCGA Glioblastoma Multiforme (GBM) dataset**, focusing on **Proneural (PN) vs Mesenchymal (ME) transcriptional subtypes**.

Covers:

-   Quality Control (QC)

-   Exploratory Data Analysis (EDA)

-   Differential Expression (DE) Analysis

-   Pathway Enrichment

-   Cellular Deconvolution, and

-   Multivariate Survival Analysis (Cox Proportional Hazards Model),

demonstrating the **complete computational biology workflow for bulk RNA-seq tumor subtype analysis**.

## Key Results

+------------------------+------------------------------------------------------------------------------------+
| Analysis               | Finding                                                                            |
+:=======================+:===================================================================================+
| Samples (post-QC)      | 180 primary GBM tumors                                                             |
|                        |                                                                                    |
|                        | -   55 PN                                                                          |
|                        |                                                                                    |
|                        | -   125 ME                                                                         |
+------------------------+------------------------------------------------------------------------------------+
| DE genes (ME vs PN)    | 2,658 significant genes                                                            |
|                        |                                                                                    |
|                        | -   1,528 up in ME, 1,130 up in PN                                                 |
|                        |                                                                                    |
|                        | <!-- -->                                                                           |
|                        |                                                                                    |
|                        | -   \>94% DESeq2/EdgeR consensus                                                   |
+------------------------+------------------------------------------------------------------------------------+
| ME upregulated theme   | Mesenchymal/wound-healing program                                                  |
|                        |                                                                                    |
|                        | -   immune infiltration, cytokine signaling, ECM remodeling                        |
+------------------------+------------------------------------------------------------------------------------+
| PN upregulated theme   | Neural identity                                                                    |
|                        |                                                                                    |
|                        | -   axonogenesis, synapse assembly                                                 |
|                        |                                                                                    |
|                        | Cell cycle proliferation                                                           |
|                        |                                                                                    |
|                        | -   chromosome segregation, nuclear division                                       |
+------------------------+------------------------------------------------------------------------------------+
| Dominant ME cell types | MES-like neoplastic cells, TAMs, Microglia, T/B/NK cells, Endothelial, Mural cells |
+------------------------+------------------------------------------------------------------------------------+
| Dominant PN cell types | NPC/OPC-like neoplastic cells, Neurons, Oligodendrocytes, Radial glia              |
+------------------------+------------------------------------------------------------------------------------+
| Survival (KM)          | Significant PN vs ME difference                                                    |
|                        |                                                                                    |
|                        | -   log-rank `p=0.033`                                                             |
+------------------------+------------------------------------------------------------------------------------+
| Survival (Cox)         | Age at diagnosis dominant death predictor                                          |
|                        |                                                                                    |
|                        | -   Hazard Ratio (HR)=1.045/year                                                   |
|                        |                                                                                    |
|                        | -   `p=1.08e-07`                                                                   |
|                        |                                                                                    |
|                        | Subtype NOT a significant predictor                                                |
|                        |                                                                                    |
|                        | -   Hazard Ratio (HR)=1.079                                                        |
|                        |                                                                                    |
|                        | -   `p=0.831`                                                                      |
+------------------------+------------------------------------------------------------------------------------+

## Repository Structure

```         
Bulk-RNAseq-TCGA-GBM/
├── 01_data/
│   ├── 01_raw/                    # Downloaded TCGA-GBM data (generated by pipeline)
│   └── 02_processed/              # Intermediate RDS files (generated by pipeline)
|
├── 02_notebooks/
│   ├── 00_setup_project_env.qmd
│   ├── 01_download_raw_data.qmd
│   ├── 02_prepare_dataset.qmd
│   ├── 03_perform_qc.qmd
│   ├── 04_perform_eda.qmd
│   ├── 05_perform_de_analysis.qmd
│   ├── 06_perform_pathway_enrichment.qmd
│   ├── 07_perform_deconvolution.qmd
│   ├── 08_integrate_and_interpret_findings.qmd
│   └── 09_project_summary.qmd
|
├── 03_figures/                    # All plots generated by pipeline
├── 04_results/                    # All results CSVs and RDS files generated by pipeline
│
├── .gitignore
└── README.md
```

## Dataset

**TCGA-GBM**: The Cancer Genome Atlas Glioblastoma Multiforme cohort

-   **Downloaded programmatically** via `TCGAbiolinks`
-   **Bulk RNA-seq** data
-   **Expression data:** Unstranded raw counts matrix, primary tumor samples only
-   **Clinical data:** Patient survival, age at diagnosis, and paper-curated subtype labels (Verhaak et al. 2010)
-   **Post-QC dataset:** 180 samples × 16,164 protein-coding genes (55 PN, 125 ME)

## Installation

### Prerequisites

-   **R** 4.5.3+
-   **RStudio** (recommended) or any R environment
-   **Quarto** for rendering notebooks

### Key R Packages

+--------------------------+---------------+-----------------------------------------------+
| Package                  | Version       | Purpose                                       |
+:=========================+:==============+:==============================================+
| `TCGAbiolinks`           | 2.38.0        | TCGA data download and preparation            |
+--------------------------+---------------+-----------------------------------------------+
| `DESeq2`                 | 1.50.2        | Primary differential expression analysis      |
+--------------------------+---------------+-----------------------------------------------+
| `edgeR`                  | 4.8.2         | Confirmatory differential expression analysis |
+--------------------------+---------------+-----------------------------------------------+
| `clusterProfiler`        | 4.18.4        | ORA and GSEA pathway enrichment               |
+--------------------------+---------------+-----------------------------------------------+
| `GSVA`                   | 2.4.4         | Per-sample pathway activity scoring           |
+--------------------------+---------------+-----------------------------------------------+
| `MCPcounter`             | 1.2.0         | Cell type deconvolution                       |
+--------------------------+---------------+-----------------------------------------------+
| `survival` + `survminer` | 3.8.6 + 0.5.2 | Survival analysis and visualization           |
+--------------------------+---------------+-----------------------------------------------+
| `tidyverse`              | 2.0.0         | Data manipulation and visualization           |
+--------------------------+---------------+-----------------------------------------------+
| `broom`                  | 1.0.13        | Tidy model outputs into clean dataframes      |
+--------------------------+---------------+-----------------------------------------------+

### Tested On
- **CPU:** 16 logical cores (Intel Core i7-13620H, 13th Gen)
- **RAM:** 7.6 GB available (WSL2 allocation; host machine has 16 GB)
- **OS:** Windows 11 with WSL2 (Ubuntu)
- **GPU:** NVIDIA RTX 4050 (not used in this project)

### Setup

1.  **Clone the repository**

``` bash
git clone https://github.com/Shirshak52/Bulk-RNAseq-TCGA-GBM.git
cd Bulk-RNAseq-TCGA-GBM
```

2. **Create the conda environment**
```bash
conda env create -f environment.yml
conda activate gbm_project_env
```

## Usage

Execute notebooks sequentially (00 → 09). Each notebook saves intermediate outputs consumed by the next.

+-------------------------------------------+-----------------------------------------------------------------+
| Notebook                                  | Description                                                     |
+:==========================================+:================================================================+
| `00_setup_project_env.qmd`                | Project directory setup, package verification                   |
+-------------------------------------------+-----------------------------------------------------------------+
| `01_download_raw_data.qmd`                | TCGA-GBM counts matrix and clinical metadata download           |
+-------------------------------------------+-----------------------------------------------------------------+
| `02_prepare_dataset.qmd`                  | SummarizedExperiment preparation, counts/metadata extraction    |
+-------------------------------------------+-----------------------------------------------------------------+
| `03_perform_qc.qmd`                       | Subtype/gene filtering, low-expression and outlier removal      |
+-------------------------------------------+-----------------------------------------------------------------+
| `04_perform_eda.qmd`                      | PCA, scree plot, PC-level pathway enrichment                    |
+-------------------------------------------+-----------------------------------------------------------------+
| `05_perform_de_analysis.qmd`              | DESeq2 + EdgeR DE analysis, volcano plots, consensus gene lists |
+-------------------------------------------+-----------------------------------------------------------------+
| `06_perform_pathway_enrichment.qmd`       | ORA + GSEA against <GO:BP> and KEGG databases                   |
+-------------------------------------------+-----------------------------------------------------------------+
| `07_perform_deconvolution.qmd`            | MCPcounter deconvolution with GBM-specific marker sets          |
+-------------------------------------------+-----------------------------------------------------------------+
| `08_integrate_and_interpret_findings.qmd` | GSVA, correlation heatmap, KM + Cox survival analysis           |
+-------------------------------------------+-----------------------------------------------------------------+
| `09_project_summary.qmd`                  | End-to-end project summary with all figures                     |
+-------------------------------------------+-----------------------------------------------------------------+

## Method Overview

### Project Pipeline Architecture

<p align="center">
<img src="gbm_project_pipeline_flowchart.png" alt="Project Pipeline Flowchart" width="50%"/>
</p>

### Analytical Decisions

-   **Subtype focus**: Restricted to **Proneural (PN) and Mesenchymal (ME) subtypes**, the two **most biologically distinct and clinically relevant** GBM subtypes per Verhaak et al. (2010)

-   **DE consensus**: **Intersection of DESeq2 and EdgeR results (\>94% overlap)** used as the **primary gene list**, ensuring findings are robust to method choice

-   **Pathway databases**: [**GO:BP**](GO:BP){.uri} and **KEGG** used throughout, consistent across EDA, pathway enrichment, and GSVA

-   **Deconvolution marker gene sets**:

    -   **Primary set**:
        -   GBM-specific **neoplastic state markers**: Neftel (2019)
        -   **Immune/stromal markers**: Moreno (2023)
    -   **Confirmatory set**:
        -   GBM-specific **neoplastic state markers**: Moreno (2023)
        -   **Immune/stromal markers**: Moreno (2023)

    chosen to reflect the **single-cell-informed understanding of GBM cellular composition.**

-   **Cox variable selection**: Hybrid of:

    -   **Literature-informed** inclusion (for subtype, age)

    -   **Data-driven greedy forward selection** with **pairwise correlation thresholds**, for:

        -   **GSVA pathways**: max rho \< 0.8, min informativeness \> 0.15

        -   **Deconvolution cell types**: max rho \< 0.7, min informativeness \> 0.3

## Key Findings

### Differential Expression

-   1,528 genes **upregulated in ME**
-   1,130 genes **upregulated in PN**
-   `padj < 0.05`, `|log2FC| > 1`
-   **confirmed independently** by DESeq2 and EdgeR with **\>94% consensus**

### Pathway Enrichment

-   **ME upregulated**: **Mesenchymal/wound-healing** program
    -   Leukocyte migration, cytokine signaling, ECM remodeling, adaptive immunity
    -   Reflects a **permanently active wound-healing-like state** consistent with the **"wound that never heals" phenomenon** in cancer biology
-   **PN upregulated:**
    -   **ORA**: **Neural identity** program
        -   Axonogenesis, synapse assembly, CNS neuron differentiation
    -   **GSEA**: **Cell cycle/proliferation** program
        -   Chromosome segregation, nuclear division, DNA damage response

### Deconvolution

-   **ME tumors:** Enriched for **MES-like neoplastic cells** and **broad immune/stromal infiltrate** (TAMs, Microglia, T/B/NK cells, Endothelial, Mural cells)
-   **PN tumors:** Enriched for **NPC/OPC-like neoplastic cells** and **neural cell types** (Neurons, Oligodendrocytes, Radial glia)
-   Both primary (Neftel + Moreno) and confirmatory (Moreno + Moreno) marker sets produced consistent results

### Integration & Survival

-   **Myeloid lineage cells** (TAM, Microglia, Monocytes, DC) specifically **drive the ME immune/wound-healing pathway signal**
    -   Confirmed by **per-sample GSVA-deconvolution correlation within both subtypes**
-   **Subtype survival difference** (KM log-rank `p=0.033`) **disappears in multivariate Cox model** (subtype HR=1.079, `p=0.831`)
    -   The **effect is mediated through biological variables**, particularly **age (HR=1.045/year, `p=1.08e-07`)** and **immune pathway activity (HR=2.879, `p=0.074`, trending)**
-   **Proportional hazards assumption verified** (global Schoenfeld `p=0.210`)

## Reproducibility

**Expected runtime:** **~45 minutes to 1 hour for the complete pipeline** (Notebooks 00–09), run sequentially **on the tested hardware specifications above**.

**Note:** `01_download_raw_data.qmd` and `02_prepare_dataset.qmd` require an **active internet connection** and **GDC portal access**. **All subsequent notebooks run entirely offline** from saved intermediate files.

## Data Sources, Tools, and References

-   **Primary dataset and patient metadata:** TCGA-GBM via GDC portal, accessed through `TCGAbiolinks`
-   **GBM Subtype Framework:** [*Integrated genomic analysis identifies clinically relevant subtypes of glioblastoma characterized by abnormalities in PDGFRA, IDH1, EGFR, and NF1*](https://www.doi.org/10.1016/j.ccr.2009.12.020) (Verhaak et al., 2010)
-   **Single-cell GBM States:** [*An Integrative Model of Cellular States, Plasticity, and Genetics for Glioblastoma*](https://doi.org/10.1016/j.cell.2019.06.024) (Neftel et al., 2019)
-   **Deconvolution Marker Gene Sets:** [GBMDeconvoluteR GitHub](https://github.com/GliomaGenomics/GBMDeconvoluteR/tree/main)
-   **Key Analysis Tools:** `TCGAbiolinks`, `DESeq2`, `edgeR`, `clusterProfiler`, `GSVA`, `MCPcounter`, `survival`, `survminer`
-   **Pathway Databases:** <GO:BP> (Gene Ontology Consortium), KEGG (Kyoto University)

## Contact

-   **Author:** Shirshak Aryal
-   **Email:** [shirshak.acad\@gmail.com](mailto:shirshak.acad@gmail.com){.email}

## License

This project is licensed under the MIT License — see LICENSE file for details.
