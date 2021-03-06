Please store third party libraries source code here. 

# How to build libpng libraries
To build libpng (and zlib) for PC linux and AM5728, please ensure they are placed at 
/home/luba/libpng-1.6.34
/home/luba/zlib-1.2.8
and TI-SDK at
/home/luba/ti-processor-sdk-linux-am57xx-evm-04.03.00.05
If you prefer your own place, the following script need to be modified accordingly.

## Build for ubuntu linux
Please copy both of libpng-1.6.34 and zlib-1.2.8 to a local filesystem 
(not remote access to Windows, because you won't be able to create symlink in windows)

Terminal A: (build libz)
```
cd zlib-1.2.8
rm -rf build
mkdir build
cd build
cmake ..
make
```
Terminal B: (build libpng)
```
cd libpng-1.6.34
rm -rf build
mkdir build
cd build
cmake .. -DZLIB_LIBRARY=/home/luba/zlib-1.2.8/build/libz.a -DZLIB_INCLUDE_DIR=/home/luba/zlib-1.2.8/build 
```
for debug:
```
cmake .. -DCMAKE_BUILD_TYPE=DEBUG -DPNG_DEBUG=1 
```
for release:
```
cmake .. -DCMAKE_BUILD_TYPE=RELEASE -DPNG_DEBUG=0
make 
```
Static library libpng16D.a can be found in /libpng-1.6.34/build
Rename it to libpng16.a, then copy to Extlibs/libpng/Linux/Debug(/Release for release version) in malibu repository.

## Build for AM5728
Terminal A: (build libz)
```
source /home/luba/ti-processor-sdk-linux-am57xx-evm-04.03.00.05/linux-devkit/environment-step
cd zlib-1.2.8
rm -rf build
mkdir build
cd build
cmake ..
make
```
Terminal B: (build libz)
```
source /home/luba/ti-processor-sdk-linux-am57xx-evm-04.03.00.05/linux-devkit/environment-step
cd libpng-1.6.34
rm -rf build
mkdir build
cd build
cmake .. -DZLIB_LIBRARY=/home/luba/zlib-1.2.8/build/libz.a -DZLIB_INCLUDE_DIR=/home/luba/zlib-1.2.8/build 
cmake .. -DM_LIBRARY=/home/luba/ti-processor-sdk-linux-am57xx-evm-04.03.00.05/linux-devkit/sysroots/armv7ahf-neon-linux-gnueabi/usr/lib/libm.so
```
for debug:
```
cmake .. -DPNG_DEBUG=1
cmake .. -DCMAKE_BUILD_TYPE=DEBUG
```
for release:
```
cmake .. -DPNG_DEBUG=0
cmake .. -DCMAKE_BUILD_TYPE=RELEASE
make 
```
Static library libpng16.a can be found in /libpng-1.6.34/build
copy to Extlibs/libpng/AM5728/Debug(/Release for release version) in malibu repository.

## For windows

Open libpng-1.6.34\projects\vstudio\vstudio.sln in visual studio
compile as normal for debug and release
copy libpng16.lib to Extlibs/libpng/AM5728/Debug(/Release for release version) in malibu repository.
