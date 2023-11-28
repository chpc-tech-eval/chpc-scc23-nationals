OpenFOAM
===========

Open FOAM is an Open-Source Computational Fluid Dynamics (CFD) is a C++ toolbox for the development of customized numerical solvers, and pre-/post-processing utilities for the solution of continuum mechanics problems. The code is typically memory bandwidth limited, such that memory channels are more useful than sheer core count.

The Linear Algebra core libraries are the main communication bottlenecks for the scalability of the linear solvers, where memory bandwidth is the predominant limiting factor.

# Installation

Follow the [general installation instructions](https://openfoamwiki.net/index.php/Installation).

## System Requirements

In order to successfully build OpenFOAM, you will require a *functioning* `C++14` compiler, as well as the *GNU* `make` build tool chain. The following table lists the most basic dependencies and their minimum version requirements:

| Program  | Version | Description                                |
| ---      |     --- | ---                                        |
| gcc      |   7.5.0 | higher version recommended                 |
| cmake    |     3.8 | required for ParaView and CGAL builds      |
| boost    |    1.48 | required for functionality and CGAL builds |
| fftw     |   3.3.7 | required for functionality                 |
| paraview |   5.6.3 | required for visualization                 |
|          |         |                                            |

## Downloading the source code

The source tarballs can be downloaded from the [Official OpenFOAM Repositories](https://dl.openfoam.com/source/latest/). You must build and configure *v2306*.

```bash
$ wget https://dl.openfoam.com/source/v2306/OpenFOAM-v2306.tgz
$ wget https://dl.openfoam.com/source/v2306/ThirdParty-v2306.tgz
```
Untar these to your desired installation location.

## Building and deploying OpenFOAM

A number of the dependencies for OpenFOAM can be built automatically during compilation. These options can be specified within the build configuration: 

```bash
$ source <INSTALLATION_PATH>/OpenFOAM-v2306/etc/bashrc
```

You can switch to the main OpenFOAM directory using `$WM_PROJECT_DIR`. Should this variable be undefined, you have a poorly configured environment. Compile OpenFOAM using :
```bash
$ # -s switch denotes --silent and -l --logging, -j (compile using specified number of cores) see ./Allwmake --help for more options
$ ./Allwmake -s -l -j <N>
```

## Post-compilation Verification

Validate the build in a new shell, after sourcing the OpenFOAM environment using:
```bash
$ foamInstallationTest
```

Verify the installation using a simple Tutorial Test case:

```bash
$ foamTestTutorial -full incompressible/simpleFoam/pitzDaily
```

The above should work, unless your environment has not been sourced correctly, in which case try to run the test tutorial benchmark manually:
```bash
# Create the user "run" directory:
mkdir -p "$FOAM_RUN"
# Change to the user "run" directory:
run
# Copy tutorial
cp -r "$FOAM_TUTORIALS"/incompressible/simpleFoam/pitzDaily ./
# Run the tutorial
( cd pitzDaily && blockMesh && simpleFoam )

```

# Benchmark: Simple Small (Serial)

Copy the benchmark from your competition USB flash drive *(Tip: Use a separate sub-folder for each case)*:
```bash
$ cp <path to USB>/OpenFOAM/SimpleBenchmarkSmall.tar.gz ~/<path to benchmark>
```

Untar the tarball and edit the configuration files as follows.

Ensure that the decomposition method is set to scotch and that the number of subdomains is 1, by editing `system/decomposeParDict`: 

```config
method scotch;
numberOfSubdomains 1; 
```

Copy the model’s geometry and surface properties from the resources directory: 

```bash
$ cp $FOAM_TUTORIALS/resources/geometry/motorBike.obj.gz constant/triSurface/ 
```

Proceed to extract the model’s surface features and prepare it to be decomposed into a mesh that will be used to numerically solve the problem case:

```bash
$ surfaceFeatureExtract
$ blockMesh
$ decomposePar
$ snappyHexMesh -overwrite
``` 

Configure the initial conditions at time step 0, and execute the  test case: 
```bash
$ rm -rf 0
$ cp -r 0.orig 0
$ simpleFoam | tee singleCore.out 
```

# Benchmark: Parallel Efficiency Investigation *[4%]*

Parallel computing can be carried out in two ways:
- One is done on a single computer with multiple internal processors, known as a ***Shared Memory Multiprocessor**.
- The other way is achieved through a series of computers interconnected by a network, known as a **Distributed Memory Multicomputer**.

OpenFOAM uses **MPI** and **POSIX threads (pthreads)** to implement a hybrid parallelism scheme. This allows message passing between **NUMA** domains, with each domain containing multiple worker threads and utilizing shared memory. 

Repeat the previous benchmark, with increasing numbers of subdomains, i.e set to 2, 6, 12, 24, etc...  This time you will execute the test case with `mpi`:
```bash
$ mpirun <MPIPARMS> simpleFoam -parallel > parallel-smp-<CORES>.out 
```

Plot a graph of the number of **cores (subdomains)** versus the reported wall time, in seconds. 

In order to determine the most efficient configuration of **MPI rank** and **pThreads**, you will need to conduct an investigation. You will do so by populating a table similar to the one shown below: 

| Total MPI Ranks | Ranks Per Node | Threads/Rank | RAM Usage Per Node | Run Time |   |   |
|             --- |            --- |          --- | ---                | ---      |   |   |
|               6 |              2 |            8 | ???                | ???      |   |   |
|              12 |              4 |            4 | ???                | ???      |   |   |
|              24 |              8 |            2 | ???                | ???      |   |   |
|          etc... |            ... |          ... | ...                | ...      |   |   |
|                 |                |              |                    |          |   |   |

You are required to submit your (1) graph and (2) all output files for your SMP runs, as well as your (3) table and (4) SLURM batch*(if you used a scheduler)* and (5) output files of your most efficient run, for judging.

# Visualization *[2%]*

Make use of `ParaView` to visualize the benchmark.

# Benchmark: Simple Large *[4%]*











