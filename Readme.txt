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
glibc revision: 2.22
binutils revision: 2.25.1
Linux kernel version: 2.6.32.x
dmalloc version: 5.5.2
ltrace version: 0.7.3
strace version: 4.10
sysroot build for headers and libs.
dependencies: cygwin1.dll. You need to install cygwin and add this dll path to $PATH.

cross-compiler build check: readelf -a Linpack_x86-Linux (extract)
ELF Header:
  Magic:   7f 45 4c 46 01 01 01 00 00 00 00 00 00 00 00 00 
  Class:                             ELF32
  Data:                              2's complement, little endian
  Version:                           1 (current)
  OS/ABI:                            UNIX - System V
  ABI Version:                       0
  Type:                              EXEC (Executable file)
  Machine:                           Intel 80386
  Version:                           0x1

Displaying notes found at file offset 0x00000148 with length 0x00000020:
  Owner                 Data size	Description
  GNU                  0x00000010	NT_GNU_ABI_TAG (ABI version tag)
    OS: Linux, ABI: 2.6.32

Get the cross compiler tool chain for windows on github:
git clone https://github.com/Cheb57/i686-nptl-linux-gnu.git 

Have a nice build and enjoy your linux cross compilation !

Regards,
Rabia Chebah.
