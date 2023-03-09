# Various ID generation algorithms...
_... for unique IDs with interesting properties._

| Algorithm | Binary size | Textual size | Features | Crates |
| --- | --- | --- |
| [Snowflake] | 64 bits | 16[^1] bytes | sortable | [snowflaked], [hexafreeze] |
| [xid] | 96 bits | 20 bytes | sortable | [libxid] |
| [MongoID] | 96 bits | 24 bytes | sortable | ... |
| [ULID] | 128 bits | 26 bytes | sortable | [ulid][ulid-rs], [rustly_ulid], [ulid-lite] |
| [UUID v4] | 128 bits | 36 bytes | | ... |

[^1]: No canonical representation.

<!-- Links: specs, overviews, or canonical implementation -->

[MongoID]: https://docs.mongodb.org/manual/reference/object-id/
[Snowflake]: https://github.com/twitter-archive/snowflake/tree/snowflake-2010
[ULID]: https://github.com/ulid/spec
[UUID v4]: https://en.wikipedia.org/wiki/Universally_unique_identifier#Version_4_(random)
[xid]: https://github.com/rs/xid

<!-- Links: Rust crates -->

[hexafreeze]: https://docs.rs/hexafreeze
[libxid]: https://docs.rs/libxid
[rustly_ulid]: https://docs.rs/rustly_ulid
[snowflaked]: https://docs.rs/snowflaked
[ulid-lite]: https://docs.rs/ulid-lite
[ulid-rs]: https://docs.rs/ulid-rs
