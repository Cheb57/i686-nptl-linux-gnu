README:
x86 cross compiler tool chain for linux under windows (gcc tool chain revision 5.2 from July 2015)


Hello,

I successfully built a cross compiler tool chain using the last ct-ng from the git repo.
It was not easier as the host is cygwin and the environment offered is not compatible with ct-ng.
So need to update the binutils for host script, ltrace/strace makefiles and the glibc source taken, to build without errors.

The details:
host: x86 cygwin
target: i686 Linux Native POSIX Thread Library (NPTL)
gcc tool chain revision 5.2.0 (July 2015) for last standards (c++11 and 14) including c/c++/gfortran compilers
gdb/gdbserver revision 7.10 for debugging
glibc revision: 2.21
binutils revision: 2.25.1
Linux kernel version: 4.2.0 mainline
dmalloc version: 5.5.2
ltrace version: 0.7.3
strace version: 4.10
sysroot build for headers and libs.
dependencies: cygwin1.dll. You need to install cygwin and add this dll path to $PATH.

Comparison of the linpack code build using a native compiler under x86 debian (gcc 4.8.3) and this cross compiler (gcc 5.2.0) using together my Intel(R) Atom(TM) CPU  330 @ 1.60GHz:

native: file Linpack 
Linpack: ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.32, BuildID[sha1]=caf65e1fbeb87e2538492c11e69f52a3dc196d98, stripped

cross-compiler: file Linpack_x86-Linux 
Linpack_x86-Linux: ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 4.2.0, stripped

native build execution: ./linpack
Enter array size (q to quit) [200]:  
Memory required:  315K.


LINPACK benchmark, Double precision.
Machine precision:  15 digits.
Array size 200 X 200.
Average rolled and unrolled performance:

    Reps Time(s) DGEFA   DGESL  OVERHEAD    KFLOPS
----------------------------------------------------
      64   0.56  87.10%   2.71%  10.19%  174302.654
     128   1.12  87.10%   2.70%  10.20%  174240.975
     256   2.25  87.09%   2.71%  10.20%  173831.153
     512   4.50  87.10%   2.70%  10.20%  174066.800
    1024   9.02  87.07%   2.74%  10.19%  173650.955
    2048  18.01  87.09%   2.72%  10.19%  173936.063


cross-compiler build execution (-O3, -march=atom, -s options build) : ./Linpack_x86-Linux 
Enter array size (q to quit) [200]:  
Memory required:  315K.


LINPACK benchmark, Double precision.
Machine precision:  15 digits.
Array size 200 X 200.
Average rolled and unrolled performance:

    Reps Time(s) DGEFA   DGESL  OVERHEAD    KFLOPS
----------------------------------------------------
      64   0.53  86.52%   2.69%  10.79%  184645.205
     128   1.07  86.52%   2.70%  10.78%  184425.140
     256   2.14  86.50%   2.70%  10.79%  184320.523
     512   4.27  86.53%   2.70%  10.77%  184676.630
    1024   8.54  86.52%   2.70%  10.78%  184572.720
    2048  17.10  86.52%   2.70%  10.78%  184390.573

cross-compiler build check: readelf -a Linpack_x86-Linux (extract)
En-tête ELF:
  Magique:   7f 45 4c 46 01 01 01 00 00 00 00 00 00 00 00 00 
  Classe:                            ELF32
  Données:                          complément à 2, système à octets de poids faible d'abord (little endian)
  Version:                           1 (current)
  OS/ABI:                            UNIX - System V
  Version ABI:                       0
  Type:                              EXEC (fichier exécutable)
  Machine:                           Intel 80386
  Version:                           0x1

Displaying notes found at file offset 0x00000148 with length 0x00000020:
  Propriétaire         Taille des données       Description
  GNU                  0x00000010       NT_GNU_ABI_TAG (étiquette de version ABI)
    OS: Linux, ABI: 4.2.0

Get the cross compiler tool chain for windows on github:
git clone https://github.com/Cheb57/i686-nptl-linux-gnu.git 

Have a nice build and enjoy your linux cross compilation !

Regards,
Rabia Chebah.
