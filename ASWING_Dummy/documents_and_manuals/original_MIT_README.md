# ASWING

General
-------
ASWING and its plot library should compile on any Unix system 
with normal Fortran-77, C, and X-Windows support.  So far,
ASWING has been used on the following systems:

* Alpha
  SGI
* Sun
* RS/6000
* HP-9000
* Pentium/Linux 
* Pentium/NT   (with X-windows emulation)
* MAC_OS 10.x
* Ubuntu Linux

The systems marked with "*" have peculiar features which require slight 
modifications to the Makefiles in the plotlib/ and bin/ directories.  
Examine these Makefiles before building the plot library and ASWING.


ARPACK linking
--------------
ASWING's eigenmode analysis module employs the ARPACK sparse eigenpackage,
developed by Sorensen and co-workers at Rice University.  This package
must be obtained if you wish to perform eigenmode analyses in ASWING.  

The ARPACK library, with literature and documentation, is available 
by anonymous ftp from:         ftp.caam.rice.edu
or via the WWWeb from:   ftp://ftp.caam.rice.edu/pub/software/ARPACK

I can provide the ARPACK package if you have trouble downloading it
from the ftp site. 


Build sequence
--------------

1)  To install, first build the single-precision 
plot library in  ./plotlib  ...

 % cd plotlib
 % make          (creates libPlt.a)


2) If you do NOT wish to perform eigenmode analyses, skip to 3).

Otherwise you must download and build the ARPACK library in 
a convenient separate directory, for example

 /usr/whatever/ARPACK/

which will also be specified in step 4).

The ARPACK package comes with README files which have directions 
for building ARPACK.  Aswing uses only the "complex16" subset of 
ARPACK's library.  So in  ARPACK/Makefile  you can set 

  PRECISIONS = complex16

which makes the resulting subset-library file much smaller 
than the complete version.  The size of the Aswing executable 
is unaffected, though.  

Warning:
The LAPACK source file ARPACK/LAPACK/dlamch.f sometimes compiles
incorrectly, causing ARPACK to hang up in an infinite loop.  
This is apparently due to some combination of tricky code and 
excessive optimization performed by the latest compilers.  
It appears on both Gfortran and Ifort compilers, and goes away 
when optimization is disabled.  In any case, the problem is solved 
in  ARPACK/Makefile  by modifying the "lib: ..." line, and adding 
the "noopt: ..." definition as follows:


lib: noopt arpacklib

noopt:
	$(CD) $(LAPACKdir); \
	$(ECHO) Making dlamch.o in $(LAPACKdir); \
	$(FC) -c -O0 dlamch.f; \
	$(CD) ..;


ARPACK sans bug is then built with the usual command:

% make lib


3) In  ./bin/Makefile  select the appropriate real-time clock routine.

For g77 or gfortran compiler:

 % SECONDS = seconds_g77.f
 
For ifort compiler:

 % SECONDS = seconds_ifc.f

Other compilers may require other system clock routine calls in ./src/seconds*.f
Edit as needed.


4) If you skipped step 2) above and do not have an ARPACK library,
select the dummy routine in ./bin/Makefile ...

  ARLIB = arpack0.o

Otherwise, specify the ARPACK library that you built in step 2):

  ARLIB = /usr/whatever/ARPACK/libarpack_machine.a


5) Build ASWING in the ./bin directory ...

 % make aswing



Documentation
-------------
User Guide is in the  aswing_doc.txt  file.  Theory documents are in the
PostScript files  

 tex/asw.pdf
 tex/aswu.pdf
 tes/dataflow.pdf


For the impatient, you can just run ASWING from the runs/ directory, 
which contains a few input files *.asw

 % cd runs
 % ../bin/aswing

The files session*.txt  contain keyboard inputs for a typical interactive 
session.  If one is lost when running ASWING, typing a "?" at any command 
prompt, e.g.  

 .OPER  c>  ?  

will always produce a keyboard command menu.



Please report bugs and suggestions to:  drela@mit.edu

