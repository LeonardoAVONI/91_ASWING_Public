# 📘 INSTALL.md — How to Build ASWING on Ubuntu/Debian

**Author:** Leonardo Avoni  
**Date:** September 2025  
**Contact:** [avonileonardo@gmail.com](mailto:avonileonardo@gmail.com)

---
## 0. Introduction

The following install file is written for an installation that uses **global libraries** for ARPACK, LAPACK, BLAS, and X11. It is also possible, though more complicated, to install ASWING with a folder-provided ARPACK. No computational differences have been observed between the two methods.

This procedure was written and tested in Ubuntu 24.04.3 LTS, on a Dell Precision 7550, Intel® Core™ i7-10850H × 12 with 32.0 GiB or RAM

## 1. Checking the folder structures
Before going any further, we need to check if the structure of the ASWING folder is as described below. Note that more folders can be present

~~~
ASWING_Repository/
├── src/                     # ASWING Fortran source
├── plotlib/                 # Plotlib source
├── bin/                     # Executable output
├── test_run/                # Test folder
├── documents_and_manuals/   # Original MIT documents
├── install_and_uninstall/   # New install and uninstall guides
├──  ...
~~~


---

## 2. Install required system packages
Open a terminal in `ASWING_repository` and run:

```bash
sudo apt update
sudo apt install     gfortran     make     build-essential     libarpack2-dev     liblapack-dev     libblas-dev     libx11-dev     git
```


> ✅ These provide the Fortran compiler, build tools, ARPACK/LAPACK/BLAS math libraries, and X11 (needed for graphics).

It is possible to check if the main packages have been installed, and where by running the following commands. Note however that this will not guarantee that hose will be the actual libraries used by ASWING's executable (unlike the `ldd` command below)

```bash
dpkg -L libarpack2-dev | grep '\.so' 
dpkg -L liblapack-dev | grep '\.so' 
dpkg -L libblas-dev | grep '\.so' 
dpkg -L libx11-dev | grep '\.so'
```

---

## 3. Build the plotting library (Plotlib)
ASWING uses its own local plotting library (in `plotlib/`).  
You need to build it before compiling ASWING. The idea is that the default makefile for the Single Precision build will be used. From the `ASWING_repository` location, type the following:

```bash
cd plotlib
cp config.make.SP config.make
make clean && make
cd ..
```

This will generate a `.a` (binary file) static library as follows: 
```
plotlib/libPlt_gSP.a
```

---

## 4. Build ASWING
You can then proceed and compile ASWING. To do so, from the `ASWING_repository`, change to the `bin` folder, then `make`. You may need to `make clean` (deleting previous install files if a previously compiled ASWING exists).

```bash
cd bin
make
```

The executable `aswing` will be created in the `bin` directory.

> ✅ For faster compiling, one can try multithreading, through `make -j x`. The value of `x` depends on the maximum number of threads of your hardware.

---

## 5. Run ASWING
It is now possible to run ASWING, using a terminal opened from the `bin/` directory, by typing the following:

```bash
./aswing
```

> ⚠️ By default, the Makefile tries to install ASWING into `/home/codes/bin`.  
> If you don’t want this, make sure the line with `install -s aswing $(BIN)` in `bin/Makefile` is **commented out**.

---

## 6. (Optional) Add ASWING to your PATH
If you want to call `aswing` from anywhere:

```bash
echo 'export PATH=$PATH:$/path/to/aswing/bin' >> ~/.bashrc
source ~/.bashrc
```

Now you can just type `aswing` in any terminal. In case several versions of ASWING are present on the same machine, this option is not recommended, as it could cause confusion about which version is being used.

---

## 7. Check linked libraries
To verify ASWING is correctly linked to system ARPACK, LAPACK, BLAS, and X11, you can type using a terminal opened from the `bin` directory:

```bash
ldd aswing | grep -E "arpack|lapack|blas|X11"
```

You should see something like:

```
libarpack.so.2 => /lib/x86_64-linux-gnu/libarpack.so.2
liblapack.so.3 => /lib/x86_64-linux-gnu/liblapack.so.3
libblas.so.3   => /lib/x86_64-linux-gnu/libblas.so.3
libX11.so.6    => /lib/x86_64-linux-gnu/libX11.so.6
```

---
## 8. Test ASWING

Move to the `test_run` folder and perform tests 1, 2, 3 as described by `test_run/Readme.md`

---
✅ That’s it! You now have a clean ASWING install using system ARPACK/LAPACK and the local Plotlib.
