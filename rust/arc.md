# Deep dive into `std::sync::Arc`

See Nomicon's chapter on [Implementing Arc].

[Implementing Arc]: https://doc.rust-lang.org/nomicon/arc.html
[drop check]: missing

## The `Arc<T>` structure

```rust
pub struct Arc<T: ?Sized> {
    ptr: NonNull<ArcInner<T>>,
    phantom: PhantomData<ArcInner<T>>,
}
```

### The `?Sized` bound on `T`

`Arc` works with any `T`, even if `!Sized` [...]

### The `NonNull<ArcInner<T>>` pointer

`NonNull<T>` has two purposes.  The first is that it specifies that the pointer
is never null and, thus, that null can be used as niche, allowing the compiler
to optimize the layout of something like `Option<Arc<T>>` to consume no extra
memory for the discriminant.

The second is that is makes `Arc<T>` covariant over `T`: if some `T` is a
subtype of some `U`, then `Arc<T>` will be a subtype of `Arc<U>`.  In a concrete
example, this makes `Arc<&'static str>` a subtype of `Arc<&'a str>`, for any
`'a`.

### The `PhantomData<ArcInner<T>>`

`PhantomData<ArcInner<T>>` is used to tell the compiler that `Arc` may – and the
last one will – drop the inner `ArcInner<T>`, even though `Arc` only stores a
pointer, which does not imply ownership.  This information is used by the
compiler for the [drop check], and is necessary because the `Drop`
implementation for `Arc` uses `#[may_dangle]`, signaling that it does not access
[...]


```
#[repr(C)]
struct ArcInner<T: ?Sized> {
    strong: atomic::AtomicUsize,

    // the value usize::MAX acts as a sentinel for temporarily "locking" the
    // ability to upgrade weak pointers or downgrade strong ones; this is used
    // to avoid races in `make_mut` and `get_mut`.
    weak: atomic::AtomicUsize,

    data: T,
}
```
