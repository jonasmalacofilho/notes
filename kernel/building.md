Building
========

Data for clangd LSP client
--------------------------

```
make compile_commands.json
```


Cross-compiling with GCC
------------------------

### Arm64/Aarch64

```
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- defconfig
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- -j12
```

`ARCH` and `CROSS_COMPILE` can be passed through the environment.


Clang
-----
_`Documentation/kbuild/llvm.rst`_
_https://www.kernel.org/doc/html/latest/kbuild/llvm.html#cross-compiling_

```
make CC=clang defconfig
make CC=clang -j12
```

**Note:** passing `CC` in the environment does *not* work.


virtme
------

```
virtme-configkernel --defconfig
virtme-configkernel --update
virtme-configkernel --arch <ARCH> --defconfig
```
