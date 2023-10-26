kcbench results
===============

calvin
------

```
# 2023-03-08
$ kcbench --src 6.2.2
[NOTE] Downloading source of Linux 6.2.2; this might take a while... 
Processor:           Intel(R) Core(TM) i7-8700K CPU @ 3.70GHz [12 CPUs]
Cpufreq; Memory:     powersave [intel_pstate]; 32034 MiB
Linux running:       6.2.2-arch1-1 [x86_64]
Compiler:            gcc (GCC) 12.2.1 20230201
Linux compiled:      6.2.2 [/home/jonas/.cache/kcbench/linux-6.2.2]
Config; Environment: defconfig; CCACHE_DISABLE="1"
Build command:       make vmlinux
Filling caches:      This might take a while... Done
Run 1 (-j 12):       190.81 seconds / 18.87 kernels/hour [P:994%, 1571 maj. pagefaults]
Run 2 (-j 12):       190.90 seconds / 18.86 kernels/hour [P:994%, 1535 maj. pagefaults]
Run 3 (-j 15):       190.77 seconds / 18.87 kernels/hour [P:998%, 406 maj. pagefaults]
Run 4 (-j 15):       190.18 seconds / 18.93 kernels/hour [P:1001%, 403 maj. pagefaults]
Run 5 (-j 6):        290.98 seconds / 12.37 kernels/hour [P:547%, 1474 maj. pagefaults]
Run 6 (-j 6):        292.18 seconds / 12.32 kernels/hour [P:548%, 1665 maj. pagefaults]
Run 7 (-j 9):        227.29 seconds / 15.84 kernels/hour [P:788%, 1108 maj. pagefaults]
Run 8 (-j 9):        225.03 seconds / 16.00 kernels/hour [P:785%, 1092 maj. pagefaults]
```

hobbes
------

```
# 2023-03-08
$ kcbench --src 6.2.2
kcbench --src 6.2.2
[NOTE] Downloading source of Linux 6.2.2; this might take a while... 
Processor:           Intel(R) Core(TM) i7-8550U CPU @ 1.80GHz [8 CPUs]
Cpufreq; Memory:     powersave [intel_pstate]; 15893 MiB
Linux running:       6.2.2-arch1-1 [x86_64]
Compiler:            gcc (GCC) 12.2.1 20230201
Linux compiled:      6.2.2 [/home/jonas/.cache/kcbench/linux-6.2.2]
Config; Environment: defconfig; CCACHE_DISABLE="1"
Build command:       make vmlinux
Filling caches:      This might take a while... Done
Run 1 (-j 8):        439.95 seconds / 8.18 kernels/hour [P:746%, 524 maj. pagefaults]
Run 2 (-j 8):        441.47 seconds / 8.15 kernels/hour [P:745%, 552 maj. pagefaults]
Run 3 (-j 10):       442.81 seconds / 8.13 kernels/hour [P:748%, 249 maj. pagefaults]
Run 4 (-j 10):       441.74 seconds / 8.15 kernels/hour [P:750%, 305 maj. pagefaults]
Run 5 (-j 4):        507.06 seconds / 7.10 kernels/hour [P:387%, 405 maj. pagefaults]
[ ... remaining runs aborted due to a unexpected supend ... ]
```
