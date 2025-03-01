# `cuRAND to oneMKL RNG Migration` Sample

The `cuRAND to oneMKL RNG Migration` Sample is a collection of code samples that demonstrate the cuRAND equivalent SYCL API functionality in the Intel® oneAPI Math Kernel Library (oneMKL). 

| Area                   | Description
|:---                    |:---
| What you will learn    | How to migrate cuRAND API based source code to the equivalent SYCL*-compliant oneMKL Interfaces API for random number generation (RNG)
| Time to complete       | 30 minutes
| Category               | Code Optimization

For more information on oneMKL and complete documentation of all oneMKL routines, see https://www.intel.com/content/www/us/en/developer/tools/oneapi/onemkl-documentation.html.

## Purpose

The sample source code using SYCL was migrated from CUDA source code for offloading computations to a GPU/CPU. The sample demonstrates migrating code to SYCL, optimizing the migration steps, and improving execution time.

Each cuRAND sample source file shows the usage of different oneMKL RNG domain routines. All are basic programs demonstrating the usage for a single method of generating pseudorandom numbers.

>**Note**: This sample is based on the [*cuRAND Library - APIs Examples*](https://github.com/NVIDIA/CUDALibrarySamples/tree/master/cuRAND) samples in the NVIDIA/CUDALibrarySamples GitHub repository.

## Prerequisites

| Optimized for         | Description
|:---                   |:---
| OS                    | Ubuntu* 20.04
| Hardware              | 10th Gen Intel® processors or newer
| Software              | Intel® oneAPI DPC++/C++ Compiler

## Key Implementation Details

This sample contains two sets of sources in the following folders:

| Folder Name             | Description
|:---                     |:---
| `01_sycl_dpct_output`   | Contains initial output of the Intel® DPC++ Compatibility Tool used to migrate SYCL-compliant code from CUDA code. <br> It may contain not fully migrated or incorrectly generated code that has to be manually fixed before it is functional. (The code does not work as supplied.)
| `02_sycl_dpct_migrated` | Contains SYCL to CUDA migrated code generated using the Intel® DPC++ Compatibility Tool with the manual changes implemented to make the code fully functional.

These functions are classified into eight different directories, each based on an RNG engine. There are **48** samples:

## Set Environment Variables

When working with the command-line interface (CLI), you should configure the oneAPI toolkits using environment variables. Set up your CLI environment by sourcing the `setvars` script every time you open a new terminal window. This practice ensures that your compiler, libraries, and tools are ready for development.

## Build the `cuRAND Migration` Sample

> **Note**: If you have not already done so, set up your CLI
> environment by sourcing  the `setvars` script in the root of your oneAPI installation.
>
> Linux*:
> - For system wide installations: `. /opt/intel/oneapi/setvars.sh`
> - For private installations: ` . ~/intel/oneapi/setvars.sh`
> - For non-POSIX shells, like csh, use the following command: `bash -c 'source <install-dir>/setvars.sh ; exec csh'`
>
> For more information on configuring environment variables, see *[Use the setvars Script with Linux* or macOS*](https://www.intel.com/content/www/us/en/develop/documentation/oneapi-programming-guide/top/oneapi-development-environment-setup/use-the-setvars-script-with-linux-or-macos.html)*.

### On Linux*

1. Change to the sample directory.
2. Build the samples.
   ```
   $ mkdir build
   $ cd build
   $ cmake ..
   $ make
   ```

   By default, this command sequence builds the version of the source code in the  `02_sycl_dpct_migrated` folder.

#### Troubleshooting

If an error occurs, you can get more details by running `make` with
the `VERBOSE=1` argument:
```
make VERBOSE=1
```
If you receive an error message, troubleshoot the problem using the **Diagnostics Utility for Intel® oneAPI Toolkits**. The diagnostic utility provides configuration and system checks to help find missing dependencies, permissions errors, and other issues. See the [Diagnostics Utility for Intel® oneAPI Toolkits User Guide](https://www.intel.com/content/www/us/en/develop/documentation/diagnostic-utility-user-guide/top.html) for more information on using the utility.


## Run the `cuRAND Migration` Sample

### On Linux

Run the programs on a CPU or GPU. Each sample uses a default device, which in most cases is a GPU.

1. Run the samples in the `02_sycl_dpct_migrated` folder.
   ```
   make run_mt19937_uniform
   ```

### Build and Run the `cuRAND Migration` Sample in Intel® DevCloud (Optional)

When running a sample in the Intel® DevCloud, you must specify the compute node (CPU, GPU, FPGA) and whether to run in batch or interactive mode. For more information, see the Intel® oneAPI Base Toolkit [Get Started Guide](https://devcloud.intel.com/oneapi/get_started/).

#### Build and Run Samples in Batch Mode (Optional)

You can submit build and run jobs through a Portable Bash Script (PBS). A job is a script that submitted to PBS through the `qsub` utility. By default, the `qsub` utility does not inherit the current environment variables or your current working directory, so you might need to submit jobs to configure the environment variables. To indicate the correct working directory, you can use either absolute paths or pass the `-d \<dir\>` option to `qsub`.

1. Open a terminal on a Linux* system.
2. Log in to Intel® DevCloud.
   ```
   ssh devcloud
   ```
3. Download the samples.
   ```
   git clone https://github.com/oneapi-src/oneAPI-samples.git
   ```
4. Change to the sample directory.
5. Configure the sample for a GPU node and choose the backend as OpenCL.
   ```
   qsub  -I  -l nodes=1:gpu:ppn=2 -d .
   export SYCL_DEVICE_FILTER=opencl:gpu
   ```
   - `-I` (upper case I) requests an interactive session.
   - `-l nodes=1:gpu:ppn=2` (lower case L) assigns one full GPU node.
   - `-d .` makes the current folder as the working directory for the task.

     |Available Nodes  |Command Options
     |:---             |:---
     | GPU	           |`qsub -l nodes=1:gpu:ppn=2 -d .`
     | CPU	           |`qsub -l nodes=1:xeon:ppn=2 -d .`

6. Perform build steps as you would on Linux.
7. Run the programs.
8. Clean up the project files.
   ```
   make clean
   ```
9. Disconnect from the Intel® DevCloud.
   ```
   exit
   ```

## Example Output

This is example output if you built the default and ran `run_mt19937_uniform`.

```
Scanning dependencies of target mt19937_uniform
[ 50%] Building CXX object 02_sycl_dpct_migrated/mt19937/CMakeFiles/mt19937_uniform.dir/mt19937_uniform.cpp.o
[100%] Linking CXX executable ../../bin/mt19937_uniform
[100%] Built target mt19937_uniform
Host
0.966454
0.778166
0.440733
0.116851
0.007491
0.090644
0.910976
0.942535
0.939269
0.807002
0.582228
0.034926
=====
Device
0.966454
0.778166
0.440733
0.116851
0.007491
0.090644
0.910976
0.942535
0.939269
0.807002
0.582228
0.034926
=====
[100%] Built target run_mt19937_uniform
```

## License

Code samples are licensed under the MIT license. See
[License.txt](https://github.com/oneapi-src/oneAPI-samples/blob/master/License.txt) for details.

Third party program licenses are at [third-party-programs.txt](https://github.com/oneapi-src/oneAPI-samples/blob/master/third-party-programs.txt).
