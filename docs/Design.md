DESIGN DOCUMENT
===============

Last edited: Jan 10, 2022 (WYP)

---

# Batch meta-script

## Phase 1: Detect cluster/system

   Cluster configs are YAML files.
   Fallback to interactive if unable to auto-detect
   Output of phase 1 is a set of vars

## Phase 2: Generate script to setup env based on template

   Read script templates into multiline Bash var, filling in the templates
   using the set of vars from phase 1
   Outputs two scripts for phases 3 & 4
   The first one is plain Bash, the second one is Slurm

## Phase 3: Run the env script

   No need to invoke `sbatch` yet!
   This part will probably perform `conda activate moa-gemm` as well.

## Phase 4: `sbatch` the Slurm script

   This script will *both* compile and run.
   The result is a __single__ `csv` database file.
   The naming convention for this `csv` file includes the following things:
   - Experiment date and time
   - Experiment details (e.g who ran it, where it was ran,
                             what kind of experiment)
   Note to self: Need to wait till `makefile` branch is merged?

## Phase 5: Housekeeping

   Tar and compress the results, and the env/module logs.
   Copy result tarball to specified directory.

---

# Plotting meta-script

## Phase 1: Detect cluster/system

   Same as above.

## Phase 2: Generate script to setup env based on template

   Notably, the script to `conda activate moa-gemm`.

## Phase 3: Read plot config

   What is x axis, y axis? What are the different curves?
   Plot labels? Legend labels? Title?
   TODO: Agree on config format

## Phase 4: Read `csv` database and extract desired 2-column data
  
   Use `pandas` to filter the database and extract the desired 2 columns
   per dataset.

## Phase 5: Call backend to plot
   For now, backend can be `gnuplot` or `matplotlib`

## Phase 5: Postprocessing

---

# Credits

Thanks to Brad Richardson (@everythingfunctional) for helping me kick-start
this document.
