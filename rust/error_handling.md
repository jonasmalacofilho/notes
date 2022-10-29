Error handling
==============

Enumeration
-----------

When the caller:

- might be able to resolve the issue;
- and differentiating between the various error scenarios is relevant.

```rust
use std::error::Error;
use std::fmt;

fn do_something(i: I) -> Result<O, SomeError> {
    todo!()
}

// Ideally: Error + Send + Sync + 'static.
#[derive(Debug)]
enum SomeError {
    // ...
}

impl fmt::Display for SomeError {
    fn fmt(&self, f: &mut fmt::Formatter<'_>) -> fmt::Result {
        // a lowercase description without trailing punctuation
        todo!()
    }
}

impl Error for SomeError {
    fn source(&self) -> Option<&(dyn Error + 'static)> {
        todo!()
    }
}
```

Opaque errors
-------------

When the caller:

- might be able to resolve the issue;
- but knowing the exact nature of the problem isn't helpful.

If there really isn't anything useful to report about the error cause/location,
then type erasure is a good alternative:

```rust
use std::error::Error;

// The 'static bound allows downcasting.
fn do_something(i: I) -> Result<O, Box<dyn Error + Send + Sync + 'static>> {
    todo!()
}
```

Another alternative is a custom ZST, which can (unlike `Box<dyn Error>`)
implement `Error`:

```rust
// Ideally: Error + Send + Sync + 'static.
#[derive(Debug)]
struct SomeError;
```

When a bit of information is of interest to the caller (e.g. line number of the
failure), an opaque type can be used:

```rust
// Ideally: Error + Send + Sync + 'static.
#[derive(Debug)]
struct SomeError {
    // ...
}

impl SomeError {
    fn line_number(&self) -> usize {
        todo!()
    }
}
```

Fallible but no meaningful error
--------------------------------

When the caller might be able to resolve the issue:

```rust
fn do_something(i: I) -> Result<O, ()> {
    todo!()
}
```

(But `()` doesn't implement `Error`; an opaque error type might be better).

(For another approach, see `Error::downcast`, which returns
`Result<Box<T>, Box<dyn Error>>`).

When the callee has nothing to return, and/or when the caller isn't expected to
handle the failure case:

```rust
fn do_something(i: I) -> Option<O> {
    todo!()
}
```

(E.g. `slice::get`, `Error::downcast_ref`)

When the only path for return is an error:

```rust
fn do_something(i: I) -> Result<!, SomeError> {
    todo!()
}
```

When the `Result` is only needed for signature compatibility:

```rust
fn do_something(i: I) -> Result<O, !> {
    todo!()
}
```

When the error is some unpredictable panic:

```rust
// std::thread::Result
pub type Result<T> = Result<T, Box<dyn Any + Send + 'static>>;
```
