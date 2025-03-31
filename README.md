# Code Folder Overview

This folder contains three core `.Rmd` notebooks that perform distinct parts of the analysis on CTCF motif intervals and whole-genome bisulfite sequencing (WGBS) data.

---

## 1) **CTCF_motif_overlap.Rmd**
- **Purpose**: Creates the four TFBS categories (`coad_only`, `coad_plus_others`, `common_all_8`, `all_w_o_coad`) by overlapping single-cancer intervals. It also imports the WGBS data (normal and tumor samples) for further modeling.  
- **Key Steps**:
  1. **Reading** merged/“cleaned” motif data for 8 cancers, merging intervals per cancer.
  2. **Defining** the logic to split COAD intervals into *COAD-only*, *COAD+*, *common all 8*, etc.
  3. **Overlapping** intervals with other data sources (e.g., JASPAR FIMO motifs) if needed.
  4. **Modeling/Analysis**: The majority of the final analyses for the paper (e.g., coverage-weighted regression, linear modeling with rank/fimo/nCpG, etc.) occur here.

If you want to replicate the main figures and results in the paper regarding TFBS categories in colon vs. other cancers, **start** with this `.Rmd`.

---

## 2) **WGBS_pwd_comparison.Rmd**
- **Purpose**: Focuses on a random sampling (e.g., 10,000 intervals) from each pairwise WGBS comparison, exploring average/median PWD (pairwise distance in DNA methylation).  
- **Key Steps**:
  1. **Randomly sampling** intervals from the large WGBS dataset to reduce computational load.
  2. **Calculating** average, median PWD, coverage, etc. per sample pair (5 tumor pairs + 1 normal pair).
  3. **Comparisons**: Quick EDA or simple comparisons of normal vs. tumor PWD on the random subset.

This `.Rmd` is **lighter** than the main analysis—useful for quick checks of how PWD behaves without fully enumerating millions of intervals.

---

## 3) **WGBS_Summarization.Rmd**
- **Purpose**: A more general **EDA** (exploratory data analysis) on the WGBS data for five cancer pairs and one normal pair. Includes reading, summarizing coverage/beta values, and computing basic statistics.  
- **Key Steps**:
  1. **Summaries** of coverage, depth, fraction of CpGs with ≥5 coverage, average/median Beta, etc.
  2. **Summaries** of the CTCF intervals from the “Science paper” dataset, e.g., the proportion of intervals that belong to each cancer, how many overlap FIMO, etc.
  3. **Basic EDA**: Checking distributions of coverage/beta across samples.

This notebook helps confirm data quality and gives background info before the more detailed analysis in `CTCF_motif_overlap.Rmd`.

---

## Getting Started

1. **Clone or download** this repository.
2. **Open** each `.Rmd` in RStudio (or another R Markdown-compatible environment).
3. **Run** them in the following order if replicating the paper’s final results:
   1. `WGBS_Summarization.Rmd` to get an overview and basic EDA.
   2. `CTCF_motif_overlap.Rmd` to define the TFBS categories and run the primary modeling.
   3. `WGBS_pwd_comparison.Rmd` if you want a smaller sampling approach to check average/median PWD quickly.

---

## Dependencies

- **R version**: 4.x or higher recommended.
- **R Packages**: `data.table`, `dplyr`, `GenomicRanges`, `GenomeInfoDb`, `ggplot2`, etc.  
  (See each `.Rmd`'s header or setup chunk for complete library calls.)

---

## Contact

For questions about these notebooks or the data, please contact Yichen Guo at guoyiche@usc.edu. 
