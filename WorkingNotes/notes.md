# SYCL Tutorial by Codeplay 

```sh
git clone --recursive https://github.com/codeplaysoftware/syclacademy.git 

cd syclacademy
export SYCLACADEMY_ROOT=`pwd`
export SYCLACADEMY_ROOT=/home/jsrobin/git/codeplaysoftware/syclacademy

```


Documentation for AdaptiveCpp: https://adaptivecpp.github.io/AdaptiveCpp/

> `source /opt/intel/oneapi/setvars.sh`



## Configuring using CMake

> `-DSYCL_ACADEMY_ENABLE_SOLUTIONS=ON`

### Additional cmake arguments for oneAPI

> `-DCMAKE_C_COMPILER=icx -DCMAKE_CXX_COMPILER=icpx`
> `-DSYCL_ACADEMY_USE_DPCPP=ON`
> `-DSYCL_ACADEMY_INSTALL_ROOT={/opt/intel/oneapi|/usr/local/acpp/20240415}`
> `-DCUDA_DIR=/usr/local/cuda`
> `-DROCM_DIR=<parth to rocm>`
> `-DSYCL_TRIPLE={amdgcn-amd-amdhsa|nvptx64-nvidia-cuda|spir64_gen|native_cpu}`

> `-DSYCL_ARCH={gfx90a|sm_90|sm_89}`




### Additional cmake arguments for AdaptiveCpp

> `-DSYCL_ACADEMY_USE_ADAPTIVECPP=ON`
`-DSYCL_ACADEMY_INSTALL_ROOT={/opt/intel/oneapi|/usr/local/acpp/20240415}`
> `-DCUDA_DIR=/usr/local/cuda`
> `-DROCM_DIR=<parth to rocm>`

Older versions may require:
> `-DACPP_TARGETS=<target specification>`
> `<target specification>="item1;item2;..."` 

where itemj from set: {omp,generic,hip:gfx90a,cuda:sm_90}

## Example of compilation

```sh
alias oneapi='source /opt/intel/oneapi/setvars.sh'
source /opt/intel/oneapi/setvars.sh
export SYCLACADEMY_ROOT=/home/jsrobin/git/codeplaysoftware/syclacademy
```


cd ${SYCLACADEMY_ROOT}/Code_Exercises/What_is_SYCL
From README.md
Verify functioning of compilers and support systems:

acpp-info
sycl-ls

cd ${SYCLACADEMY_ROOT}
cmake --preset Isycl > cmake.Isycl.config.log 2>&1 ; sleep 3 ; less +F cmake.Isycl.config.log
cmake --build --preset Isycl   > cmake.Isycl.build.log 2>&1 ; sleep 3 ; less +F cmake.Isycl.build.log

cmake --preset Asycl > cmake.Asycl.config.log 2>&1 ; sleep 3 ; less +F cmake.Asycl.config.log
cmake --build --preset Asycl   > cmake.Asycl.build.log 2>&1 ; sleep 3 ; less +F cmake.Asycl.build.log



[Introduction to SYCL](https://tech.io/playgrounds/48226/introduction-to-sycl/introduction-to-sycl-2)

