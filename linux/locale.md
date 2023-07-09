A quasi-international en_US locale
==================================

TL;DR:

```
LANG=en_US.UTF-8
LC_PAPER=en_GB.UTF-8
LC_MEASUREMENT=en_GB.UTF-8
LC_TIME=en_AG.UTF-8
```

---

Start of with the `en_US.UTF-8` locale:

```
LANG=en_US.UTF-8
```

For numeric, monetary, paper and measurements, use `en_GB`:

```
LC_PAPER=en_GB.UTF-8
LC_MEASUREMENT=en_GB.UTF-8
```

Using `en_GB` for time would cause weeks to start at Mondays, which I find weird (at least in
calendars). Instead, use `en_AG`:

```
LC_TIME=en_AG.UTF-8
```
