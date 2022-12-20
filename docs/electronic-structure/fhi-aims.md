# FHI-aims

[FHI-aims. All-electron electronic structure theory with numeric atom-centered orbitals.](https://fhi-aims.org/)

FHI-aims is used within the group primarily to perform DFT calculations for metallic systems.
In particular, our electronic friction calculations are performed using the implementation within FHI-aims.

## How to compile FHI-aims

### 1: Clone FHI-aims from GitLab

FHI-aims is hosted in a private GitLab repository.
First, set up a GitLab account, then email email kokott@fhi-berlin.mpg.de or aims-coordinators@fhi-berlin.mpg.de and ask for access to the FHI-aims GitLab repository.

Once you have been given access:

1. Open a terminal on your chosen HPC system via SSH `ssh username@avon.scrtp.warwick.ac.uk`.
2. Clone the FHI-aims repository: `git clone https://aims-git.rz-berlin.mpg.de/aims/FHIaims.git` 

### 2: Load the necessary modules

Before it is possible to compile the code you must load the relevant compilers and libraries.
On most HPC systems this is done using the `module` command.

#### Avon modules

```bash
module load iccifort/2019.5.281 impi/2019.7.217 imkl/2019.5.281
module load GCCcore/9.3.0
module load CMake/3.16.4
```

#### Sulis modules

```bash
module load foss/2021b
module load CMake
```

### 3: Configure CMake

Move into the FHI-aims directory with `cd` then run
```bash
mkdir build
cd build
touch initial.cmake
```

This will create the build directory containing an empty file `initial.cmake`.
By setting variables inside `initial.cmake` you are able to configure the build to your system.

#### Example `initial.cmake`

##### Avon

```makefile
set(CMAKE_Fortran_COMPILER mpiifort CACHE STRING "" FORCE)
set(CMAKE_Fortran_FLAGS "-O3 -fp-model precise" CACHE STRING "" FORCE)
set(Fortran_MIN_FLAGS "-O0 -fp-model precise" CACHE STRING "" FORCE)
set(LIB_PATHS "$ENV{MKLROOT}/lib/intel64" CACHE STRING "" FORCE)
set(LIBS "mkl_intel_lp64 mkl_sequential mkl_core mkl_blacs_intelmpi_lp64 mkl_scalapack_lp64" CACHE STRING "" FORCE)
set(CMAKE_C_COMPILER icc CACHE STRING "" FORCE)
set(CMAKE_C_FLAGS "-O3 -ip -fp-model precise" CACHE STRING "" FORCE)
```

##### Sulis

```makefile
set(CMAKE_Fortran_COMPILER mpif90 CACHE STRING "")
set(CMAKE_Fortran_FLAGS "-O3 -ffree-line-length-none -fallow-argument-mismatch " CACHE STRING "")
set(Fortran_MIN_FLAGS "-O0 -fbacktrace -ffree-line-length-none -fallow-argument-mismatch " CACHE STRING "")
set(LIBS "scalapack openblas" CACHE STRING "" FORCE)
set(USE_MPI ON CACHE BOOL "" FORCE)
set(USE_SCALAPACK ON CACHE BOOL "" FORCE)
set(USE_LIBXC ON CACHE BOOL "" FORCE)
set(USE_HDF5 OFF CACHE BOOL "" FORCE)
set(USE_RLSY ON CACHE BOOL "" FORCE)
set(CMAKE_C_COMPILER mpicc CACHE STRING "")
set(CMAKE_C_FLAGS "-O3 -funroll-loops -std=gnu99" CACHE STRING "")
```

##### Locally with Intel oneAPI
```makefile 
###############
# Basic Flags
###############
set(CMAKE_Fortran_COMPILER mpiifort CACHE STRING "" FORCE)
set(CMAKE_Fortran_FLAGS "-O3 -fp-model precise" CACHE STRING "" FORCE)
set(Fortran_MIN_FLAGS "-O0 -fp-model precise" CACHE STRING "" FORCE)
set(LIB_PATHS "/opt/intel/mkl/lib/intel64" CACHE STRING "" FORCE)
set(LIBS "mkl_intel_lp64 mkl_sequential mkl_core mkl_blacs_intelmpi_lp64 mkl_scalapack_lp64" CACHE STRING "" FORCE)

###########
# C Flags
###########
set(CMAKE_C_COMPILER icc CACHE STRING "" FORCE)
set(CMAKE_C_FLAGS "-O3 -ip -fp-model precise -std=gnu99" CACHE STRING "" FORCE)
```

##### M1 Mac
This uses the GNU compiler as Intel is not compatible on Apple silicon. It is also required to download the following packages with homebrew first:
- gcc 
- open-mpi
- openblas
- lapack
- cmake
- scalapack
```makefile
set(CMAKE_Fortran_COMPILER "mpifort" CACHE STRING "")
set(CMAKE_Fortran_FLAGS "-O3 -ffree-line-length-none -fallow-argument-mismatch" CACHE STRING "")
set(CMAKE_C_COMPILER "gcc-12" CACHE STRING "")
set(CMAKE_C_FLAGS "-O3" CACHE STRING "")

set(LIBS "blas scalapack" CACHE STRING "")
set(USE_MPI        ON CACHE BOOL "")
set(USE_SCALAPACK  ON CACHE BOOL "")
```

Run `cmake -C initial.cmake ../.` to configure your build.

### 4: Compile the code

Now that the build is configured, run `make -j 8` to compile the code. (`8` is number of processes used to compile the code).
The compiled executable `aims.$VERSION.scalapack.mpi.x` will be in `build/` directory. 

## Contribution

If you are compiling FHI-aims on a new HPC system, please update this guide to include your CMake configuration settings.
