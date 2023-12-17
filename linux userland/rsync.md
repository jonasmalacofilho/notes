# rsync

## Most used invocations

- rsync -PaHAX [--info=name0,progress2] <source>[/] <dst>/
- rsync -PaHAX <src>[/] <dst>/ -v --dry-run --delete
- rsync -PaHAX <src>[/] <dst>/ --exclude [/]<pattern> -v --dry-run --delete

Enable compression with `-z`.

## Trailing slashes

On the _source_ directory: avoid creating an additional directory level at the destination.

On the _destination_ path: copy any source items _into_ a destination directory with that name.

Without a trailing slash on the destination path, and if the transfer consists of a single item and
the last element of the destination path doesn't exist as a directory, then rsync will use that as
name the of the only item being transferred.
