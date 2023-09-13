# Batch correction and evaluation

## Motivation

Batch correction in single-cell transcriptomics mitigates unwanted technical variations inherent in single-cell RNA sequencing (scRNA-seq) data. These technical or batch effects can stem from varying experimental conditions or sequencing platforms. If left unaddressed, they can obscure genuine biological signals. To tackle this, we have incorporated several batch correction methods, including CCA, FastMNN, RPCA, and Harmony. Additionally, the pipeline can compute various quality metrics to determine which method excels for a specific dataset.

## Step-by-step

The batch module consists of two steps: batch effect correction and assessment using quality metrics. The criteria for these quality metrics were established based on the scIB publication. Additionally, we leverage kBET, a renowned method for assessing batch correction in single-cell projects.

### 1. Running pipeline

```{.bash .copy}

nextflow run single_cell_basic.nf --project_name Training --sample_csv sample_table.csv --meta_data meta_data.csv --cancer_type Ovarian -resume -profile seadragon

```

By default the previous command line considers thresholds.

!!! info "HPC"

    * `input_integration_evaluate`     = all
    * `thr_cell_proportion`            = 0.30
    * `input_lisi_variables`           = cLISI;iLISI

Alternatively, we execute this task on [Cirro](https://cirro.bio).

!!! info "Cirro"

    * `Define methods to be evaluated`              = all
    * `Cell proportion for Batch evaluation`        = 0.30
    * `Define LISI types for Density plot`          = cLISI;iLISI

### 2. Inspecting report

#### 2.1. Quality control table

#### 2.2. Before and after 

## Reference

1. [A test metric for assessing single-cell RNA-seq batch correction](https://www.nature.com/articles/s41592-018-0254-1)
2. [Benchmarking atlas-level data integration in single-cell genomics](https://www.nature.com/articles/s41592-021-01336-8)
3. [scPOP](https://github.com/vinay-swamy/scPOP)