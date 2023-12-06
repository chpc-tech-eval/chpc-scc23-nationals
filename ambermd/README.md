AmberMD
=========

[Amber](https://ambermd.org/) is a suite of biomolecular simulation programs. It began in the late 1970's, and is maintained by an active development community. The term **"Amber"** refers to two things:
* First, it is a set of molecular mechanical force fields for the simulation of biomolecules, which are available in the public domain and are used in a variety of simulation programs,
* Second, it is a package of molecular simulation programs which includes source code and demos.

**Amber** is distributed in two parts: [AmberTools23](https://ambermd.org/AmberTools.php) and [Amber22](https://ambermd.org/AmberMD.php).

# Benchmark *[10]*

Very little guidance or instructions will be given for this benchmark and you'll be required to figure out for yourselves how to build, run and compile **AmberMD**.

The [Benchmark Files](https://hpc.nih.gov/apps/amber/) are available from the data files from the Biowulf HPC Cluster at the NIH.

You are required to run:
* Explicit Solvent: JAC_Production_NPT_4fs & JAC_Production_NVE_4fs *[4%]*
* Implicit Solvent: Myoglobin *[3%]
* Implicit Solvent: Nucleosome *[3%]*

For each of the three benchmarks above, plot the results for an increasing number of CPUs used vs `ns/day` for: 2, 4, 8, 16, etc CPUs.
