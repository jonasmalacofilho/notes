Haskell
=======

Type classes (`Num`) are akin to interfaces, or Rust traits (`Add`).

Types are capitalized (`Num`), but generic types are not (`a`).  Generic types
are commonly `a`, instead of `T` in Rust/Haxe.

```haskell
add :: Num a => a -> a -> a

add x y = x + y
```

A lambda version would look like:

```haskell
let add2 = \y -> 2 + y in
                    -- ^^
                    -- after this add2 can be called

add2 3
```


Monads
------

Links:

- Sage Mitchell's 2022 talk:
  [_monads desmitified for Rustaceans curious about Haskell_](https://www.youtube.com/watch?v=4Ky8kvDcshg)
  ([slides](https://docs.google.com/presentation/d/14ZkXOf16A25HZ4zbJUK7npnFv73bl25ONTya-7Ak1iA),
  [copy](https://docs.google.com/presentation/d/1sBrpoqDXbRsJJIDAAFtO3kM4wSPyc2hX8gMjx3yD9Pc))

Rust has some monad types (`Result`, `Option`), but not a generic and higher
level concept of a monad.

### The `Maybe` monad

The `Maybe` monad is similar to Rust's `Option`:

```haskell
data Maybe a
  = Nothing
  | Just a
```

With it, the `<-` operator behaves similarly to Rust's `?` operator:
extract/unpack the inner value from a `Just`, or return `Nothing`.

```haskell
addEither :: Int -> Maybe Int -> Maybe Int

addMaybe x y = do
    y2 <- y
    Just (x + y2)
```

### The `Either` monad

The `Either Error` monad is similar to Rust's `Result`, except that the generic
parameters are swapped.

```haskell
data Either a b    -- equivalent to Rust's Result<T, E>
  = Left a         -- equivalent to Rust's Result::Error(E)
  | Right b        -- equivalent to Rust's Result::Ok(T)
```

```haskell
addEither :: Int -> Either Error Int -> Either Error Int

addEither x y = do
    y2 <- y
    Right (x + y2)
```

### The `pure` function and generic monad

A type is monadic with respect to some other type: `Maybe _`, `Either Error _`.

The `pure` function is available for all monads.

```haskell
addMonad :: Monad m => Int -> m Int -> m Int

addMonad x y = do
    y2 <- y
    pure (x + y2)
```

This will work with `Maybe a`, `Either Error a`, `[a]`, `Parser a`,
`StatefulGen g m`, `IO a`, ...

In the case of lists, monads model "non-deterministic choice": some function
`foo :: Monad a => m Int -> m Int -> m Int`, called with `foo [1, 2, 3] [10,
20]` could naturally compute (or use) the cartesian product of both lists.

### With bind

```haskell
addMonad x y =
    y >>= \y2 -> pure (x + y2)
--    ^^^
--    bind: if successfully unpacked, then call the lambda and return its result
```

### Monad laws

There are some.  Monads are _expected_ to satisfy them.

Read more about:

- `Functor a`
- `Applicative a`
- `Monad a`

Open `ghci` and execute `:doc Monad`.

### TODO

- constructor, chaining/bind function, injector function
