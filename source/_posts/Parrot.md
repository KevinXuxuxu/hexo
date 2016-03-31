# Parrot
> a journey of misery

- gcc-4.5 is needed.
  - gmp-5.1.3
    - need sth. called `m4`
    ```
    sudo apt-get install m4
    ```
  - mpfr-3.1.4
  - mpc-1.0.2
  - above packages must be installed in exact version and order
- configure and build gcc in the target folder
- possible problems
  - cannot find `crti.o`: No such file or directory
    - create symbolic link between libs
    ```
    cd /usr/lib
    ln -s x86_64-linux-gnu/crt*.o .
    ```
  - configure: error: cannot find neither zip nor jar, cannot continue
    - just get zip-3.0
    ```
    sudo apt-get install zip
    ```
  - i386:x86-64 architecture of input file `/usr/lib/../lib/crtn.o' is incompatible with i386 output
    - change default setting of gcc in file: `gcc/config/i386/t-linux64`
    ```
    # On x86-64 we do not need any exports for glibc for 64-bit libgcc_s,
    # override the settings
    # from t-slibgcc-elf-ver and t-linux
    SHLIB_MAPFILES = $(srcdir)/libgcc-std.ver \
		    $(srcdir)/config/i386/libgcc-x86_64-glibc.ver

    MULTILIB_OPTIONS = m64/m32
    MULTILIB_DIRNAMES = 64 32
    MULTILIB_OSDIRNAMES = ../lib64 ../lib
    ```
    - So changing the last row to be:
    ```
    MULTILIB_OSDIRNAMES = ../lib ../lib32
    ```
  - make: asm/errno.h: No such file or directory
    - missing package
    ```
    sudo apt-get install linux-libc-dev
    ```
- Installing built gcc-4.5.4
  - remove the old version of gcc and install the new
  ```
  sudo apt-get remove gcc
  cd gcc-obj
  make install
  ```
- Installing other packages
  - deprecating packages
    - package libtiff4-dev is deprecated in `sudo apt-get install dejagnu flex bison axel libboost-dev libtiff4-dev`, used `libtiff5-dev` instead.

- Even though I succussfully installed gcc-4.5, there's still no way for me to build `llvm` correctly. The error message even exceeded the limit of number of lines in ubuntu terminal. I'm now fully aware that I might not be able to config the environment correctly. I'm just down with it. 
