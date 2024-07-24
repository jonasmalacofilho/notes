# fish-shell

## Variable expansion and quoting

When setting the variable, quotes can make the difference between a string and a list:

```
$ set -l one "foo bar"
$ set -l two foo bar
$ printf '|%s|\n' $one
|foo bar|
$ printf '|%s|\n' $two
|foo|
|bar|
```

Whether quotes are needed when expanding a variable depends (to some extent) on whether the variable
is a string or a list. Without quotes, strings are always expanded as a single argument, while lists
will expand to multiple arguments. With quotes, even lists are expanded as a single argument:

```
$ set -l two foo bar
$ printf '|%s|\n' $two
|foo|
|bar|
$ printf '|%s|\n' "$two"
|foo bar|
```

## Command substitution and quoting

Command substitution works in a similar way to list expansion.

Without quotes (in which case both `(basename $i .jpg)` and `$(basename $i .jpg)` are supported),
the output from the inner command is split up by lines, and each line becomes an argument to the
outer command.

With quotes (where only `"$(basename $-i .jpg)"` is supported), the output from the inner command is
_not_ split up by lines. However, trailing empty lines are still removed.
