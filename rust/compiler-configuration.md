# Compiler configuration

## Passing options to rustc with RUSTFLAGS

```
$ export RUSTFLAGS="-C target-cpu=native"
$ RUSTFLAGS="-C target-cpu=native" cargo <...>
```

## Passing options to rustc with config.toml

Files: `.cargo/config.toml`, `~/.cargo/config.toml`

```toml
[target.x86_64-unknown-linux-gnu]
rustflags = [
"-C", "target-cpu=native",
]
```

## Specify linker or linker options

LLVM LLD (Linux): `-C link-arg=-fuse-ld=lld`

GCC LD.GOLD: `-C link-arg=-fuse-ld=gold`

Delegate LTO to the linker: `-C linker-plugin-lto`
