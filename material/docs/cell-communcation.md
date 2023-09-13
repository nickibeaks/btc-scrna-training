# Cell-cell communication

## Motivation

Cell-cell communication analysis offers insights into the interactions among different cell types within a tissue or tumor. These interactions form intricate networks that can reveal mechanisms associated with alterations in the tumor microenvironment and disease progression. To decipher this complex orchestration, we utilize well-established methods from the literature, specifically **CellChat** and **LIANA**.

## Step-by-step

Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.

### 1. Running pipeline

```{.bash .copy}

nextflow run single_cell_basic.nf --project_name Training --sample_csv sample_table.csv --meta_data meta_data.csv --cancer_type Ovarian -resume -profile seadragon

```
!!! info "HPC"

    * `input_cell_markers_db`    = ./assets/cell_markers_database.csv
    * `input_annotation_level`   = Major cells

Alternatively, we execute this task on [Cirro](https://cirro.bio).

!!! info "Cirro"

    * `Input cell markers`              = Default
    * `Annotation level`                = Major cells

### 2. Inspecting report

#### 2.1. LIANA output

#### 2.2. CellChat output

## Reference

1. [scTyper: a comprehensive pipeline for the cell typing analysis of single-cell RNA-seq data](https://link.springer.com/article/10.1186/s12859-020-03700-5)