## Run program with constrained resources

```
$ systemd-run --scope -p MemoryMax=4000M -p MemorySwapMax=0 -p CPUQuota=400% <program> [args..]
                         ^^^^^^^^^^^^^^^    ^^^^^^^^^^^^^^^    ^^^^^^^^^^^^^
                                          don't swap instead    % of one CPU
```

Resource control options:
https://www.freedesktop.org/software/systemd/man/systemd.resource-control.html
