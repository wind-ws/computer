
`panic!`:
- **Unwind（展开栈）**：逐层清理调用栈，运行各层的 `Drop` 实现（析构函数）。
- **Abort（中止）**：直接终止程序，不做任何清理。

debug下默认是 unwind
release可设置: `[profile.release] panic = "unwind"` 或 `"abort"`

### catch_unwind


# 参考
[std::panic - Rust](https://doc.rust-lang.org/std/panic/index.html)
