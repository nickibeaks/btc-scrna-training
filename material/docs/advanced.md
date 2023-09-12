# Advanced configuration

### 1. Creating Nextflow profiles

For users running the pipeline in an HPC environment, it is necessary to set up a profile. Essentially, Nextflow [profiles](https://www.nextflow.io/docs/latest/config.html#config-profiles) define specific settings related to the job scheduler of the HPC. Various HPCs may employ different engines for job scheduling, such as SLURM, TORQUE, and LSF. 

#### 1.1 SLURM profile

The profiles should be written on the `nextflow.config` file. For HPCs, it is essential to load the `singularity` module. This instruction will replace the `module load` command.

```{ .bash .copy }

institution {

    module = 'singularity/3.7.0'

    singularity {

        enabled      = true

    }

    process {

        executor     = 'slurm'
        queue        = 'medium'

    }

    params {

        max_memory   = 128.GB
        max_cpus     = 32
        max_time     = 24.h

    }
}

```

The previous snippet creates a profile for a institution powered by SLURM. It includes several settings, such as loading modules like `singularity/3.7.0`, and specifying the job scheduling engine with the `executor` property. Nextflow works with many engines; for more details, refer to the official [documentation](https://nf-co.re/docs/usage/tutorials/step_by_step_institutional_profile). Please note that the `process`  scope should match the HPC specs, i.e., queue, memory and cpus.

---

## 2. Adding gene signatures and meta-programs

