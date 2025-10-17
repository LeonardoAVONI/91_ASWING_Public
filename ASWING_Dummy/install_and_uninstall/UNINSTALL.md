# 📘 UNINSTALL.md — How to Uninstall ASWING on Ubuntu/Debian

**Author:** Leonardo Avoni  
**Date:** September 2025  
**Contact:** [avonileonardo@gmail.com](mailto:avonileonardo@gmail.com)

---
## 0. Introduction

The following uninstall file is written for an installation that used **global libraries** for ARPACK, LAPACK, BLAS, and X11. 

This procedure was written and tested in Ubuntu 24.04.3 LTS, on a Dell Precision 7550, Intel® Core™ i7-10850H × 12 with 32.0 GiB or RAM

---

## 1. Remove the ASWING folder and contents

Delete the entire ASWING folder, including all subfolders and files.  
> **Note:** The ASWING executable is located in the `/bin` folder.

Example (replace `ASWING_5_98` with your actual folder path):

~~~
rm -rf ~/ASWING_5_98
~~~

---

## 2. Remove dependencies (optional)

If you no longer need ASWING or related development tools, you may remove the installed system packages:

```bash
sudo apt remove --purge gfortran gcc make build-essential libarpack2-dev liblapack-dev libblas-dev libx11-dev
sudo apt autoremove --purge
```

⚠️ Be careful: removing `build-essential` will uninstall core tools like `gcc`, which are commonly needed for other projects.

---

## 3. Remove ASWING from your PATH (optional)

If you previously added ASWING to your PATH in ~/.bashrc, remove it as follows:
Open ~/.bashrc in a text editor:

```bash
nano ~/.bashrc
```

Find the line that looks like:

```bash
export PATH=$PATH:/path/to/aswing/bin
```

Delete the line or comment it out by adding # at the start:

```bash
#export PATH=$PATH:/path/to/aswing/bin
```

Save the file and exit the editor; then reload your shell configuration:

```bash
source ~/.bashrc
```

Now the aswing command will no longer be available globally.

## 4. Verify cleanup

Check whether ASWING is still available in your `PATH`:

```bash
which aswing
```

If nothing is returned, ASWING has been removed successfully.

---

**ASWING has now been fully removed from your system.**
