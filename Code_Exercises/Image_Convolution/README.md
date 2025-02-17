# SYCL Academy

## Exercise 15: Image Convolution
---

In this exercise there is no task, simply familiarize yourself with the image
convolution reference code, as this will be used in later exercises.

---

### 1.) Reference image

For the purposes of this exercise we have provided an image in the exercise
directory called "dogs.png", however feel free to replace this with any other
32bit PNG image, though note that this exercise will work best with images
where the dimensions are multiples of 2, such as 512x512.

Note you will have to update the path to an image. There is the image in the
repository but feel free to use any image you choose. Though it's recommend that
you use a png image whose dimensions are multiple of 2 (for example 512x512)
and has four channels (RGBA).

### 2.) Stb library

The source for this example provides a stub which loads and write an image using
the STB image library.

### 3.) Benchmarking

The source also contains a call to a benchmarking utility that will print the
time taken to execute the SYCL code, the SYCL code should go inside the lambda
that is passed to the `benchmark` function.

Though note that the benchmark facility provided measures whole application time
which is less accurate than measuring the kernel execution times alone.

Try running the application and recording the benchmark result timing you see so
you can compare this with results in later exercises.

Note if you are running on the host device the default iterations for the
benchmark of 100 will take a while to execute so try reducing this number.

### 4.) Dimensionality

The reference code uses a 2-dimensional `range` in `parallel_for` as this often
simplifies the code when working with images.

### 5.) Convolution filters

The image convolution support code provides a `filter_type` enum which allows
you to choose between `identity` and `blur`. The utility for generating the
filter data; `generate_filter` takes a `filter_type` and a width.

## Build and execution hints

If you haven't done so already, follow this [guide](../README.md#connecting-to-devcloud-via-ssh) to build the exercise directory structure.

## Compiling with DPC++

From the syclacademy directory
```sh
cd build/Code_Exercises/Image_Convolution
```
and execute:
* ```make Image_Convolution_reference``` - to build reference.cpp
* ```make``` - to build reference.cpp

Alternatively from a terminal at the command line:
```sh
icpx -fsycl -o Image_Convolution_reference -I../../Utilities/include/ -I../../External/stb ../Code_Exercises/Image_Convolution/reference.cpp
```

In Intel DevCloud, to run computational applications, you will submit jobs to a queue for execution on compute nodes,
especially some features like longer walltime and multi-node computation is only available through the job queue.
Please refer to the [guide][devcloud-job-submission].

So wrap the binary into a script `job_submission`
```sh
#!/bin/bash
./Image_Convolution_reference
```
and run:
```sh
qsub -l nodes=1:gpu:ppn=2 -d . job_submission
```

The stdout will be stored in ```job_submission.o<job id>``` and stderr in ```job_submission.e<job id>```.

For DPC++:
Using CMake to configure then build the exercise:
```sh
mkdir build
cd build
cmake .. "-GUnix Makefiles" -DSYCL_ACADEMY_USE_DPCPP=ON -DSYCL_ACADEMY_ENABLE_SOLUTIONS=OFF -DCMAKE_C_COMPILER=icx -DCMAKE_CXX_COMPILER=icpx
make Image_Convolution_reference
```
Alternatively from a terminal at the command line:
```sh
icpx -fsycl -o Image_Convolution_reference -I../../Utilities/include/ -I../../External/stb reference.cpp
```

For AdaptiveCpp:
```sh
# <target specification> is a list of backends and devices to target, for example
# "generic" compiles for CPUs and GPUs using the generic single-pass compiler.
# When in doubt, use "generic" as it usually generates the fastest binaries.
#
# Recent, full installations of AdaptiveCpp may not need targets to be provided,
# compiling for "generic" by default.
cmake -DSYCL_ACADEMY_USE_ADAPTIVECPP=ON -DSYCL_ACADEMY_INSTALL_ROOT=/insert/path/to/adaptivecpp -DACPP_TARGETS="<target specification>" ..
make Image_Convolution_reference
```
alternatively, without CMake:
```sh
cd Code_Exercises/Image_Convolution
/path/to/adaptivecpp/bin/acpp -o sycl-Image_Convolution_reference -I../../Utilities/include/ -I../../External/stb --acpp-targets="<target specification>" reference.cpp
```
