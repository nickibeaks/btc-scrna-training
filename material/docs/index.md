# Getting started

## Installation

### 1. Nextflow and third-party software
Nextflow can be used on any POSIX-compatible system (Linux, OS X, WSL). It requires Bash 3.2 (or later) and Java 11 (or later, up to 18) to be installed.

```{ .bash .copy }
wget -qO- https://get.nextflow.io | bash
```

### 2. Docker and Singularity
This tutorial was tested using Docker v20.10.22 and Singularity v3.7.0. Please make sure to have both software available. The btc-sc-mvp pipeline will require docker images for running.

### 3. Cloning scRNA-Seq Pipeline

```{ .bash .copy }
git clone https://github.com/WangLab-ComputationalBiology/btc-scrna-pipeline
```

### 4. Running single-cell pipeline
#### 4.1. Preparing inputs
The pipeline requires two inputs, a sample table and meta-data. Both files should follow a mandatory format as described below.

Sample table should be a csv with four columns, sample, fastq_{1,2}. The column sample will be associated with all reports across the pipeline. Also, it will be required to combine the meta-data on the Seurat object. Prefix and fastq columns are mandatory for Cellranger.

{{ read_csv('./assets/test_sample_table.csv') }}

Meta-data (.csv) should contain variables related to experimental design (e.g., batch and cell sorting status). Additionally it could have more biological information about that sample. The batch variable will be used to correct the effect. In this pipeline version, we are executing a correction based on a single variable. Finally, the sort column will be used in future editions as an additional step for the QC process.

{{ read_csv('./assets/test_meta_data.csv') }}

#### 4.2. Preparing parameters for pipeline execution
To run the pipeline, we must input three parameters: project_name, sample_csv, and meta_data. In addition, for those using the HPC environment, we need to set up a profile. Briefly, profiles are specific settings related to the job scheduler on the HPC. For instance, each HPC can rely on different engines to schedule jobs, such as SLURM, TORQUE, and LSF. Additionally, profiles can be used to store parameters, i.e., for testing purposes.

nextflow run single_cell_basic.nf --project_name <PROJECT> --sample_csv <path/to/sample_table.csv> --meta_data <path/to/meta_data.csv> -resume -profile <PROFILE>
Note: There is a semantic difference between the nextflow (-) and the pipeline (--) parameters. For instance, double-dashed parameters are restricted to pipeline logic, e.g., coded to change filters and thresholds on the single-cell analysis. Finally, the pipeline will generate a folder based on --project_name, which will hold our results after the end of the execution. The -resume command will leverage the Nextflow caching system to provide re-entrance.

#### 4.3. An example of a SLURM profile
The profiles should be written on the nextflow.config file. For HPCs, loading the singularity/3.7.0 will be mandatory. We can add information about queue size, memory, and cpus.

```{ .bash .copy }
slurm {

    module = 'singularity/3.7.0'

    singularity {
        enabled = true
    }

    process {
        executor = 'slurm'
        cpu = 24
        queue = 'medium'
        memory = '64 GB'
    }

    params {
        cpus = 24
        memory = 64
    }

}
```

#### 4.4. Shorten command-line
A huge command line can be painful. Luckily, we can shorten instructions by using Nextflow -params-file. It will be a JSON file containing all parameters for that specific run. In the case of testing parameters, it could be a good practice to generate multiple files (e.g., PARAMS_TEST_01.json, PARAMS_TEST_02.json).

```{ .bash .copy }

{
 "project_name": "BTC-DISEASE-00",
 "sample_csv": "path/to/sample_table.csv",
 "meta_data": "path/to/meta_data.csv"
}
```

In addition, we could add custom QC parameters:

```{ .bash .copy }

{
 "project_name": "BTC-DISEASE-00",
 "sample_csv": "path/to/sample_table.csv",
 "meta_data": "path/to/meta_data.csv",
 "thr_mean_reads_per_cells": 10000
}
```

```{ .bash .copy }
nextflow run single_cell_basic.nf -params-file <PARAMS.json> -resume -profile <PROFILE>
```

## Expect outputs

```{ .bash .copy }
# Output tree
```
