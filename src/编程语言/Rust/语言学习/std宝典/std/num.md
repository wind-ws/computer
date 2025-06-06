



### NonZero优化
```rust
assert_eq!(size_of::<Option<u8>>(),2);
assert_eq!(size_of::<Option<NonZeroU8>>(),1);
// Option<NonZeroU8> 无0,所以Rust将0优化为None,非0就是Some
```

# 参考
[std::num - Rust](https://doc.rust-lang.org/std/num/index.html)
