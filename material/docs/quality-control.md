# Sample and QC filtering

## Motivation

Quality control (QC) is an essential step on single cell RNA-seq projects. Low-quality cells, contaminants, and doublets can greatly impact data interpretability, i.e., concealing genuine biological signals. Additionally, QC in single-cell data is a challenging process that can only be evaluated through downstream analyses, making it an iterative procedure and case-specific. The major goals of performing QC and filtering include:

### QC Metrics and Filtering Methods

* **Filtering by UMI Counts:** This helps eliminate barcodes not representing single cells, with thresholds varying in literature.
* **Filtering by Number of Features:** Similar to UMI counts, this removes likely multiplets, but thresholds can vary.
* **Filtering by Percent of Mitochondrial (mt) Reads:** Elevated mt RNA suggests unhealthy cells; thresholds vary. Be cautious with meaningful mt gene expression.
* **Doublet Detection:** Detects multiplets using tools like DoubletFinder. Setting thresholds is subjective and data-dependent.
* **Identifying Empty Droplets:** Distinguishes cell-containing droplets from empty ones, with methods like emptyDrops and other tools available.
* **Removing Ambient RNAs:** Addresses contamination from ambient RNAs using statistical approaches.

## Hands-on

The current pipeline version covers most common QC metrics, including the parameters described below. In this tutorial, we will cover the very basic steps regarding Cellranger alignment and sample filtering.

### 1. Running pipeline using default parameters

To improve reproducibility we suggest several thresholds based on multiple reports on literature (see below). In addition, for this training we will leverage a dataset derived MSK Spectrum [[1]](https://www.nature.com/articles/s41586-022-05496-1). The dataset can be download through the BTC Buckets [[2]]().

```{.bash .copy}

nextflow run single_cell_basic.nf --project_name Training --sample_csv sample_table.csv --meta_data meta_data.csv --cancer_type Ovarian -resume -profile seadragon

```

By default the previous command line considers thresholds.

!!! Thresholds

    * `thr_estimate_n_cells` = 300
    * `thr_mean_reads_per_cells` = 25000
    * `thr_median_genes_per_cell` = 900
    * `thr_median_umi_per_cell` = 1000
    * `thr_nFeature_RNA_min` = 300
    * `thr_nFeature_RNA_max` = 7500
    * `thr_percent_mito` = 25
    * `thr_n_observed_cells` = 300

### 2. Inspecting HTML report

A fundamental component in the pipeline is related to its HTML reports generation. Over the tutorials, we will browse several HTML reports and discuss key features in each analysis.



