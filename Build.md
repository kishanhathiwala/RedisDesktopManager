#Steps to build the app
1. git clone --recursive https://github.com/uglide/RedisDesktopManager.git -b (check branch) rdm && cd ./rdm
2. Go to `3rdparty/qredisclient/3rdparty/hiredis` and apply the patch to fix compilation on Windows: `git apply ../hiredis-win.patch`
3. Go to the `3rdparty/` folder and install zlib with nuget: `nuget install zlib-msvc14-x64 -Version 1.2.11.7795`
4. Run the following commands:
```
cd 3rdparty/lz4/build/cmake
cmake -DLZ4_BUNDLED_MODE=ON  .
make
```
5. Install python and note down the version
6. update the python path in `3rdparty\pyotherside.pri` 
7. pip3 install -r src/py/requirements.txt
8. Run the following command:
```
# build lz4
cd 3rdparty/lz4/build/cmake
cmake -DLZ4_BUNDLED_MODE=ON  -G"Visual Studio 17 2022" -A x64 .  //if this line throws error follow the instruction in command prompt
cmake  -G"Visual Studio 17 2022" -A x64 .
msbuild /t:build LZ4.sln /p:Configuration="Release" //Run this line in Visual studio Developer Powershell

# build snappy
cd 3rdparty\snappy
cmake  -G"Visual Studio 17 2022" -A x64 .
msbuild /t:build Snappy.sln /p:Configuration="Release"

# build zstd
cd 3rdparty\zstd\build\cmake
cmake  -G"Visual Studio 17 2022" -A x64 .
msbuild /t:build zstd.sln

# build brotli
cd 3rdparty\brotli
cmake  -G"Visual Studio 17 2022" -A x64 .
msbuild /t:build brotli.sln /p:Configuration="Release"

# build zstd
cd 3rdparty\zstd\build\cmake
cmake  -G"Visual Studio 17 2022" -A x64 .
msbuild /t:build zstd.sln /p:Configuration="Release"
```
  
Open Qt Creator and Choose the Desktop Qt 5.15.x MSVC2019 64bit > Release build profile and build.
