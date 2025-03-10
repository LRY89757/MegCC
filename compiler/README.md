## building

megcc depend on llvm-project and megbrain, now llvm-project and megbrain are integrated by submodule, and static linked into megcc
- update third-party submodule

    $ cd megcc
    $ ./third_party/prepare.sh

- build megcc

    $ cd megcc/compiler
    $ mkdir build
    $ cmake .. -G Ninja
    $ ninja

after build the compiler tools is stored in build/tools/...

### kernel test
Ninja is recommend(make is not tested ...)
X86 test

    $ mkdir -p build_x86
    $ cd build_x86
    $ cmake ../test/kernel  -G Ninja
    $ ./megcc_test_run
ARM Android test 

    $ mkdir -p build_arm
    $ cd build_arm
    $ cmake ../test/kernel -DCMAKE_TOOLCHAIN_FILE="$NDK_ROOT/build/cmake/android.toolchain.cmake"  -DANDROID_NDK="$NDK_ROOT" -DANDROID_ABI=arm64-v8a  -DANDROID_NATIVE_API_LEVEL=21  -G Ninja -DCMAKE_BUILD_TYPE=Debug
    $ copy2phone megcc_test_run
    $ run_phone ./megcc_test_run

set environment `export extra_gtest_args="--gtest_filter=AARCH64.ConvBiasNCHWNCHW44"` will build specific kernel to save time. 

### regression test
`ninja megcc-test` or `make megcc-test`

ensure `lit` was already installed:

    $ pip3 install --user lit

and add option `-DLLVM_EXTERNAL_LIT=/path/to/lit` when cmake build

## ycm support
if you are vimer, you can use ycm, you just need
- cd compiler
- mkdir build
- building the whole compiler
