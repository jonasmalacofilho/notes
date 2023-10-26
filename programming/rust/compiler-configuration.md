# Compiler configuration

## Passing options to rustc with RUSTFLAGS

```
$ export RUSTFLAGS="-C target-cpu=native"
$ RUSTFLAGS="-C target-cpu=native" cargo <...>
```

Note that these will override any rustflags entries in `[~/].cargo/config.toml` (e.g. non-default
linkers).

## Passing options to rustc with config.toml

Files: `.cargo/config.toml`, `~/.cargo/config.toml`

```toml
[target.x86_64-unknown-linux-gnu]
rustflags = [
    # link with lld
    "-Clink-arg=-fuse-ld=lld",
    # but use --no-rosegment for better stack traces (see note on [cargo-]flamegraph's README and
    # <https://bugs.chromium.org/p/chromium/issues/detail?id=919499#c16>)
    "-Clink-arg=-Wl,--no-rosegment",
    # also optimize for this uarch
    "-Ctarget-cpu=native",
]
```

## Linker and linker options

LLVM LLD (Linux): `-Clink-arg=-fuse-ld=lld -Clink-arg=-Wl,--no-rosegment` (see note on
[cargo-]flamegraph's README).

GCC LD.GOLD: `-Clink-arg=-fuse-ld=gold`

Delegate LTO to the linker: `-Clinker-plugin-lto`

## Huge pages

[Supposedly](https://kobzol.github.io/rust/rustc/2023/10/21/make-rust-compiler-5percent-faster.html),
huge pages can make rust builds 5% faster (and up to 35% more memory hungry).

Ensure Linux [Transparent Huge Pages] are enabled (`always` or at least on `madvise`):

```
echo /sys/kernel/mm/transparent_hugepage/enabled
```

Enable rustc's [jemalloc] use of transparent huge pages for all user mappings and jemalloc metadata:

```
export MALLOC_CONF="thp:always,metadata_thp:always"
cargo build
```

[Transparent Huge Pages]: https://www.kernel.org/doc/html/latest/admin-guide/mm/transhuge.html
[jemalloc]: https://jemalloc.net/jemalloc.3.html
