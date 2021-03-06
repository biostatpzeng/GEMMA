# INSTALL GEMMA: Genome-wide Efficient Mixed Model Association

## Check version

Simply run gemma once installed

    gemma

and it should give you the version.

## GEMMA dependencies

GEMMA runs on Linux and MAC OSX and the runtime has the following
dependencies:

* C++ tool chain
* GNU Science library (GSL) 1.x (does not currently work with GSL >= 2).
* blas
* [Eigen library](http://eigen.tuxfamily.org/dox/)
* zlib

See below for installation on Guix.

## Install GEMMA

### Bioconda

(Note Bioconda install is a work in [progress](https://github.com/genetics-statistics/GEMMA/issues/52)

Recent versions of GEMMA can be installed with
[BioConda](http://ddocent.com/bioconda/) without root permissions using the following
command

    conda install gemma

### GNU Guix

The GNU Guix package manager can install recent versions of [GEMMA](https://www.gnu.org/software/guix/packages/g.html)
using the following command

    guix package -i gemma

To install the build tools with GNU Guix

    guix package -i make gcc linux-libre-headers gsl eigen openblas lapack glibc ld-wrapper

### Install from source

Install listed dependencies and run

	make -j 4

(the -j switch builds on 4 cores).

if you get an Eigen error you may need to override the include
path. E.g. on GNU Guix with shared libs and DEBUG the following may
work

	make EIGEN_INCLUDE_PATH=~/.guix-profile/include/eigen3 FORCE_DYNAMIC=1 WITH_OPENBLAS=1 DEBUG=1

to run GEMMA tests

	time make check

You can run gemma in the debugger with, for example

	gdb --args \
		./bin/gemma -g example/mouse_hs1940.geno.txt.gz \
		-p example/mouse_hs1940.pheno.txt -a example/mouse_hs1940.anno.txt \
		-snps example/snps.txt -nind 400 -loco 1 -gk -debug -o myoutput

Other options, such as compiling with warnings, are listed in the
Makefile.

## Run tests

GEMMA includes the shunit2 test framework (version 2.0).

    make check

or

    ./run_tests.sh
