# Recipes for manually building haxe and related projects

## Haxe

```
$ git pull
$ git submodules update
## optional: git submodules update --force

## optional: opam switch create 4.08.1
## optional: opam switch 4.08.1

$ eval $(opam env) && opam update && opam upgrade && opam pin add haxe . --no-action && opam install haxe --deps-only
$ make ADD_REVISION=1 -j12 haxe && make haxelib && _ make install && systemctl --user restart haxe
```

## Hashlink

```
$ git pull

$ make DEBUG=1 -j12 && _ make install
```
