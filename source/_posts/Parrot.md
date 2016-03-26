# Parrot
> a journey of misery

- gcc-4.5 is needed.
  - gmp-5.1.3
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
