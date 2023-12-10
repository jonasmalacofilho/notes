# Profiling Rust programs
_... on Linux._

Use cargo-flamegraph or perf directly.

## Tips for cargo-flamegraph

### Sample system calls

Pass `--root`.

### Observe and change the sampling frequency

Pass `-F <frequency>`.

## Keeping debuginfo in release/bench builds

It's generally beneficial to have debuginfo when profiling.

Enabling `"line-tables-only"` is enough for perf

```
# Cargo.toml

[profile.release]
debug = "line-tables-only"
```

but, cargo-flamegraph needs 1/"limited" for some reason.

```
# Cargo.toml

[profile.release]
debug = 1
```

It's also possible to this through `CARGO_PROFILE_RELEASE_DEBUG=<value>`.

## Linking with lld

When linking with lld, it might be necessary to pass `-Clink-arg=-Wl,--no-rosegment` to rustc for
better stack traces.

```
# config.toml

[target.x86_64-unknown-linux-gnu]
rustflags = [
    # link with lld
    "-Clink-arg=-fuse-ld=lld",
    # but use --no-rosegment for better stack traces (see note on [cargo-]flamegraph's README and
    # <https://bugs.chromium.org/p/chromium/issues/detail?id=919499#c16>)
    "-Clink-arg=-Wl,--no-rosegment",
]
```

See note on the [cargo-]flamegraph's README and the linked chromium bug:
<https://bugs.chromium.org/p/chromium/issues/detail?id=919499#c16>.
