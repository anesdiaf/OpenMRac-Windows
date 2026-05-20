# OpenMRac

[![OpenMRac youtube video](media/openmrac-yt.jpg)](https://youtu.be/r3hLTo5Nu1g)

OpenMRac is a split-screen racing game. It is a tweaked source release of [MultiRacer](https://www.franticware.com/multiracer).

Programming was done by Vojtěch Salajka.  
Porting to big endian architectures for Amiga-like OSes was done by [Szilárd Biró](https://github.com/BSzili).

⚠️ Beware! The source code is old and messy, plus most comments are in Czech 😁

Creating forks and porting to additional platforms is encouraged, but these typically will not be merged back to the main repo. The same applies to mods.

Franticware claims rights to the name "MultiRacer" which should not be used by other parties for their products or ports. That is the reason for changing the title to OpenMRac, to which no such restrictions apply.

Game data files are in a separate repository under a different license: https://github.com/Franticware/OpenMRac-data

# Installation Instructions

## Windows


Create new folder "OpenMRac"

Open the folder you created in the terminal.


I have created a CMakeLists.txt file inside /src to configure our build and include all the required libraries in this project.


**Prerequisites:**
* [CMake](https://cmake.org)
* [Msys2](https://www.msys2.org)
* [Ninja](https://ninja-build.org)    ```winget install Ninja-build.Ninja```  

**Let's install our libraries**

* Open msys2 Shell
```
pacman -S mingw-w64-x86_64-toolchain
pacman -S mingw-w64-x86_64-SDL2
pacman -S mingw-w64-x86_64-glew
pacman -S mingw-w64-x86_64-zlib
pacman -S mingw-w64-x86_64-libpng
pacman -S mingw-w64-x86_64-libjpeg-turbo
pacman -S mingw-w64-x86_64-openal
pacman -S mingw-w64-x86_64-glm
```

**We'll need these later to build our dat file (Game data)**
```
pacman -S make tar coreutils findutils gawk sox
```

**Let's build our executable**
```
git clone https://github.com/Franticware/OpenMRac.git
cd openmrac/src


cmake -S . -B build -G Ninja -DCMAKE_C_COMPILER=gcc -DCMAKE_CXX_COMPILER=g++
cmake --build build
```
* The game file will be in "\OpenMRac\OpenMRac\src\build\bin\OpenMRac.exe"

**Let's build our Data**

We don't need to do any converting we just need to run make to execute our makefile in "\OpenMRac\OpenMRac-data\"

* Open Mingw64 shell
```
cd [RelativePathTo OpenMRac-data]

make
```
This will create our .dat file (openmrac.dat), copy the generated file to "\OpenMRac\OpenMRac\src\build\bin\"

**Copy DLLs**

Since our executable is dynamically linked against our libraries; we need to copy some dlls to the executable folder
* SDL2.dll
* glew32.dll
* libopenal-1.dll/openal32.dll
* libwinpthread-1
* libstdc++-6
* libpng16-16
* libjpeg-8
* libgcc_s_seh-1



## Linux

### Arch-based (Arch, Manjaro, EndeavourOS, ...)

Install **openmrac** package from AUR

### Debian-based (Debian, Raspberry Pi OS, Ubuntu, MX Linux, Mint, ...)

* The openmrac and openmrac-data packages are now available in many Debian-based distributions. If not, please use method described in the following section (Other).

* Note: The openmrac-es2 package is planned (OpenGL ES 2.0 variant) which might be better suited for SBCs based on RISC-V and ARM.

### Other (openSUSE, Fedora, ...)

```
git clone https://github.com/Franticware/OpenMRac-data.git
cd OpenMRac-data
make install
cd ..

git clone https://github.com/Franticware/OpenMRac.git
cd OpenMRac/src
make -f Makefile.linux install
cd ../..
```

## Windows

## Mac OS X
TODO

# Branches

* [main](https://github.com/Franticware/OpenMRac/tree/main) - current SDL 2 version, OpenGL with shaders
* [legacy](https://github.com/Franticware/OpenMRac/tree/legacy) - older SDL 1.2 version, OpenGL 1.x (no shaders)
* [dos-3dfx](https://github.com/Franticware/OpenMRac/tree/dos-3dfx) - version for DOS with 3dfx cards, based on the legacy branch
