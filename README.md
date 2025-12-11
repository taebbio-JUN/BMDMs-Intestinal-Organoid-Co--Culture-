# BMDMs + Intestinal Organoid Co-culture mRNA Analysis

This repository contains the qPCR/mRNA summary data and R scripts used to analyze
BMDM–intestinal organoid co-culture experiments, including TNFα-induced inflammation
and intestinal stemness / regeneration markers.

---

## 1. Contents of this repository

### 1.1 Data file

- **`BMDMs + Intestinal Organoid Co- Culture mR...`**  
  Main data file (Excel/CSV) containing group-wise summary statistics for:
  - Intestinal stemness / niche genes (e.g. *Lgr5, Bmi1, Sox9, Epcam, Axin2, Wnt3a, Notch1, Hes1, Atoh1, Yap1, Wwtr1* …)  
  - Inflammatory / stress-related genes (e.g. *Tnf, Cxcl2, Il18, Ptgs2, Stat3, Mapk8, Tp53, Cleaved-cas3* …)  
  across the following conditions:
  - Control  
  - TNFα only  
  - TNFα + BMDMs (1k, 5k)  
  - BMDMs only (1k, 5k)

The table typically includes columns such as:
`group`, `mean`, `sd`, `n`, `log2FC`, `t_stat`, `df_welch`, `p_value`, `p_adj`, `stars`
(see script comments for exact structure).

---

### 1.2 R analysis scripts

> Note: File names below follow the pattern shown in the folder  
> (please adapt to your exact file names if needed).

- **`R Studio - R Code - BMDMs + TNF alpha Infla...`**  
  R script for the **TNFα inflammatory panel**:
  - Reads the mRNA/qPCR summary table  
  - Calculates log₂ fold-changes (TNFα ± BMDMs vs control)  
  - Performs Welch’s t-tests and FDR correction  
  - Generates heatmaps and/or barplots for inflammatory genes  
    (e.g. *Tnf, Cxcl2, Il18, Ptgs2, Stat3*).

- **`R studio - R Code - BMDMs + Intestinal Organ...`**  
  R script for **intestinal stemness and niche gene analysis** under
  **TNFα ± BMDMs** conditions:
  - Subsets stemness / differentiation / Hippo / Wnt / Notch genes  
  - Builds log₂ fold-change matrices (tnfa, tnfa BMDMs 1k, tnfa BMDMs 5k)  
  - Creates ComplexHeatmap-based figures with significance stars.

- **`R studio - R Code - BMDMs + Intestine Organ...`** (1)  
  R script focusing on **BMDMs-only co-culture**:
  - Compares BMDMs 1k and BMDMs 5k vs control  
  - Examines how BMDMs alone remodel stemness / apoptosis markers  
  - Outputs summary tables and heatmaps.

- **`R studio - R Code - BMDMs + Intestine Organ...`** (2)  
  Utility / extended analysis script:
  - Shared functions (data import, p-value → stars, factor ordering)  
  - Additional plots (e.g. combined figures, summary heatmaps, export to CSV).

---

## 2. R environment and dependencies

All scripts are written for R (RStudio) and use the following packages:

- Data handling  
  - `readxl`, `readr`, `dplyr`, `tidyr`, `tibble`, `stringr`, `purrr`
- Visualization  
  - `ggplot2`, `ggrepel`, `scales`
- Network / graph visualization (for pathway or gene–gene networks)  
  - `igraph`, `ggraph`
- Heatmap & advanced plots (in some scripts)  
  - `ComplexHeatmap`, `circlize`, `grid`
- Enrichment analysis (if used)  
  - `gprofiler2`

You can install all required packages with:

```r
req <- c(
  "tibble","readr","readxl",
  "dplyr","stringr","purrr","tidyr",
  "ggplot2","ggrepel","scales",
  "igraph","ggraph",
  "ComplexHeatmap","circlize","grid",
  "gprofiler2"
)

inst <- rownames(installed.packages())
if (length(setdiff(req, inst)) > 0) {
  install.packages(setdiff(req, inst), repos = "https://cloud.r-project.org")
}


## 5. Figure mapping

| Script file name                                      | Output / Usage                          |
|------------------------------------------------------|-----------------------------------------|
| R Code - BMDMs + TNF alpha Inflammation.R            | Main inflammatory heatmap  |
| R Code - BMDMs + Intestinal Organoids – Stemness.R   | Stemness / niche heatmap   |
| R Code - BMDMs + Intestine Organoids – BMDMs only.R  | BMDMs-only comparison by gProfiler2   |
| R Code - BMDMs + Intestine Organoids – BMDMs + TNF alpha .R     | BMDMs + TNF alpha comparison by gProfiler2    |


## 6. Reproducibility

- Tested with R 4.x on Windows 10
- Fonts and figure size for journal submission are specified inside each script
  (ggplot2 / ComplexHeatmap section).
- Random seeds (if any) are set via `set.seed()` in the corresponding scripts.
