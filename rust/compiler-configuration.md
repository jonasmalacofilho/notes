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
"-Ctarget-cpu=native",
]
```

## Specify linker or linker options

LLVM LLD (Linux): `-Clink-arg=-fuse-ld=lld -Clink-arg=-Wl,--no-rosegment` (see note on
[cargo-]flamegraph's README).

GCC LD.GOLD: `-Clink-arg=-fuse-ld=gold`

Delegate LTO to the linker: `-Clinker-plugin-lto`
