MILC
=====

The building blocks of all *"matter"* in the universe, are comprised of atoms. These so-called *"atoms"*, are themselves comprised of *"sub-atomic"* particles known as protons, neutrons and electrons. The *"protons"* and *"neutrons"* (or baryons) are made up of elementary particles known as **quarks** and **gluons**. Their formulation forms part of the Standard Model of particle physics, which is the theory describing three of the four known fundamental forces: the strong nuclear force, electromagnetism, and the weak nuclear force; (excluding gravity).

The MILC Code is a body of high performance research software written in C (with some C++) for doing SU(3) lattice gauge theory on high performance computers as well as single-processor workstations. A wide variety of applications are included. It's primarily used to model the strong interaction, which is responsible for confining quarks within protons and neutron. This branch of physics, is also refereed to as quantum field theory or quantum chromodynamics (QCD).

# Obtaining the source code

A copy of the source code can be obtained from GitHub:
```bash
$ git clone https://github.com/milc-qcd/milc_qcd.git
```

## Checkout the development branch

The *default* `master` branch of the repository is not well maintained. For that reason you will be working on the `development` branch:
```bash
$ cd milc_qcd
$ git checkout develop
```

# Model of Interest

A number of different models are available for running the simulation. The model that you will be building and compiling to run the benchmark, utilizes the RHMC algorithm (Rational Hybrid Monte Carlo) which in turn uses rational function approximations for the *"fermion"* determinants when generating the lattices. *(Where protons and neutrons are comprised of so-called quarks, electrons are themselves considered fundamental and are known as fermions.)*

```bash
$ cd ks_imp_rhmc
```
## Build, Configure and Compile

Copy and edit the `Makefile` from the parent directory:

```bash
$ cp ../Makefile .
```

You'll need to make the following changes:

```bash
# Bonus points wil be awarded to teams who use both GNU and Intel Compilers
COMPILER=<your compiler>
# Determine this using lscpu
ARCH=<based on your servers>
# You are NOT compiling for GPUs
WANTQUDA=false
# You can test using a serial run, but benchmark will not finish without MPI and/or OpenMP Threads
MPP =true
# You must use double-precision
PRECISION=2
OMP=true
```

After modifying all of the appropriate `make` files, build the executable binary and redirect the output to a log file:

```bash
$ make su3_rhmd_hisq 2>&1 | tee make_logfile.log
```

### Remember to Clean Build

Should you need to correct any compilation or build errors, **remember to clean build** and remove any previously built object files, before attempting to recompile:

```bash
$ make clean
rm ../libraries/*o*
```

# Benchmark: NERSC MILC *[10%]* 

You Will be using the **medium** benchmark, `36x36x36x72.chklat` for the competition.

## Obtaining the Benchmark Files

The benchmark files can be obtained from the NERSC repository. Note that this file repository included very outdated versions of the MILC source code and run scripts, so ignore these:

```bash
$ wget https://portal.nersc.gov/project/m888/apex/MILC_160413.tgz
$ tar xvzf MILC_160413.tgz
$ cd MILC-apex/benchmarks/medium
$ wget https://portal.nersc.gov/project/m888/apex/MILC_lattices/36x36x36x72.chklat
```

## Running the Benchmark

Copy your binaries and benchmark files to the correct folders. You can execute long listing from the `MILC-apex/benchmarks/medium` folder to determine where the symbolic links are expecting to find the paths.

Finally, edit and execute `run_medium.sh` for an optimal configuration of `<CORES>`, `<MPI Ranks>` and `<OpenMP Threads>` for your system.

## Submission

Submit your build script, all *'edited'* `Makefiles`, compilation log files, executable binary, `run_medium.sh` and output log files.
