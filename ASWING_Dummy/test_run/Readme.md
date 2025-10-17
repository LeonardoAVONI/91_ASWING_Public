# ASWING Test Procedure

**Author:** Leonardo Avoni  
**Date:** September 2025  
**Contact:** [avonileonardo@gmail.com](mailto:avonileonardo@gmail.com)

---

## 📌 Purpose
This folder provides a **test procedure** to verify whether the current ASWING build is working correctly and producing correct results.  

The procedure consists of **three tests** (`test1`, `test2`, `test3`) that use:  
- An aircraft geometry file: `HALE.asw`  
- A gust file: `1mcosine.gust`  

These files are **benchmarks** chosen to test functionality, not specific aircraft or gust cases.  

⚠️ **Note:** This test is **not a tutorial** on how to use ASWING. It only checks whether ASWING executes commands properly.

---

## 📂 Repository Structure

Before starting, ensure the **repository root** contains exactly:

- **Files**
  - `1mcosine.gust`
  - `HALE.asw`
  - `Readme.md`
  - `Readme.html`

- **Test Folders**
  - `test1`
  - `test2`
  - `test3`

Each test folder contains `expected_plot_testX.ps` (reference output for validation, where `X = 1–3`)  

---

## ▶️ Running the Tests
### 🔹 Introduction

1. Ensure only the required **files and folders** are present (see [Repository Structure](#-repository-structure)).  
2. Open a terminal in the `test_run` folder.  
3. Run ASWING with:  
   ```bash
   ../bin/aswing HALE

4. Copy-paste the correspondant instructions from the subsections below


> **NOTE:** If things fail to work, especially for Test 1, lowering the default window size can help. This can be done, after starting ASWING but before running the tests, by typing `PLPA`, `W`, and lowering all window sizes (to 0.5 for example)

### 🔹 Test 1: Trimming and Setup
Test 1 performs the following operations
1. Import gust file (`gget`)
2. In **PLOT menu**:  
   - Plot beamwise properties of beam 4 (fuselage: `P, 4`) → save to `plot.ps` (`H`)   
   - Plot aircraft shape (`D`) → append to `plot.ps`  
   - Plot gust velocity magnitude (`G, 8`) → append to `plot.ps` (`H`)   
3. In **OPER menu**:  
   - Set airspeed to **30 m/s** (`!V 30`)  
   - Enter constraint modification, keyboard inputs (`%`), then set:  
     - Free flight mode (`f`)  
     - Link vertical velocity(`Uz`) to vertical acceleration constraint (`a_z=0`), cell `9,3`
     - Link pitch angle(`Theta`) to longitudinal acceleration constraint (`a_x=0`), cell `17,1` 
     - Link elevator deflection (`delta_F2`) to pitch rate constraint (`alpha_y=0`) → cell `20,5`
     - Engine symmetry (`E1 → alpha_z`, enforces `E1 = E2`, cell `23,6`)  
     - Horizontal flight (`E2 → gamma=0`, cell `24,32`)  
   - Append constraints table to `plot.ps` (`H`)   
   - Run trimming point steady simulation (`x`)  
   - Retain trimming point as defaults (`R`)  
   - Append trimming point plot to `plot.ps` (`H`)   
   - Set defaults for free & frequency calculation constraints (`f`, `c`)  
4. Save results:  
   - Operation point (`psav`)  
   - Settings (`ssav`)  
   - State file (`hsav`)  
5. Quit ASWING (`QUIT`).  

The corresponding code to copy-pase to execute Test 1, after having started ASWING is the following:

~~~
gget 1mcosine.gust
plot
P
4
H
D
H
G
8
 
 
H
 
 
OPER
!V 30
%
f
9,3
17,1
20,5
23,6
24,32
 
H
x
R
H
%
f
c




psav

ssav

hsav


QUIT
 
~~~




---

### 🔹 Test 2: Unsteady Simulation
Test 2 performs the following operations
1. Load files from Test 1:  
   - State (`tget`)  
   - Operating point (`pget`) *(optional, defaults to `HALE.pnt`)*  
   - Settings (`sget`) *(optional, defaults to `HALE.set`)*  
   - Gust file (`gget`)  
2. In **OPER menu**:  
   - Select unsteady simulation (`.`)  
   - Run transient simulation (`x`) → timestep = `0.01`, iterations = `20`  
   - Save default plot to `plot.ps` (`H`)  
3. In **Parameter seq. plots (output) menu**:  
   - Select parameters (`S`) by number: `9 11 15 17 65 68 78`  
   - Plot (`P`) and append to `plot.ps` (`H`)   
4. Quit ASWING (`QUIT`).  

The corresponding code to copy-pase to execute Test 2, after having started ASWING is the following:

~~~
tget HALE.state
pget HALE.pnt
sget HALE.set
gget 1mcosine.gust
OPER
.
x
0.01 20
H
P
S
9 11 15 17 65 68 78
 
 
 
P
 
H
 
QUIT
 
~~~



---

### 🔹 Test 3: Eigenmode Analysis
Test 3 performs the following operations
1. Load files from Test 1:  
   - State (`tget`)  
   - Operating point (`pget`) *(optional, defaults to `.pnt`)*  
   - Settings (`sget`) *(optional, defaults to `.set`)*  
2. In **MODE menu** (`MODE`):  
   - New eigenmode calculation (`N`) → 16 eigenvalues, search around `(-0.1, 0)`  
   - Additional eigenmode calculation (`A`) → 16 eigenvalues, search around `(-0.1, 20)`  
   - Save root-locus plot to `plot.ps` (`H`)   
   - Return current eigenvalues (`-`)
3. Quit ASWING (`QUIT`).  

In the last lines of the terminal, before ASWING is closed, the following eigenvalues should be reported:

~~~
 .MODE (point:  1)   c>  # Flexible HALE 3, Murua et al. 2012                                              
# 
#   Op.Point     Eigenvalue
       1   -0.46111345E-02     0.0000000    
       1    0.70612490E-02    0.18467080    
       1   -0.28861594         1.1293988    
       1    -2.4765290         1.3912824    
       1    -10.180228         5.2276188    
       1    -10.718135         6.9155491    
       1    -3.6675323         13.224853    
       1    -17.492737         10.167651    
       1    -3.1788453         20.269005    
       1   -0.26202486         24.726515    
       1    -1.1428357         31.137008    
       1    -2.9256105         40.300262    
~~~

The corresponding code to copy-pase to execute Test 3, after having started ASWING is the following:

~~~
tget HALE.state
pget HALE.pnt
sget HALE.set
MODE
N
16
-0.1 0
A
16
-0.1 20
H
-

QUIT
 
~~~

---


