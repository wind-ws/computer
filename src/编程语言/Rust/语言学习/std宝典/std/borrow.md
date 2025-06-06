

### Cow
仅需要 不可变引用时,他始终保持引用
若需要 可变时,他会clone一份数据后 保持所有权

`Cow` 实现了 `Deref`，这意味着可以直接调用非可变方法


### Borrow

### BorrowMut

### ToOwned


# 参考
[std::borrow - Rust](https://doc.rust-lang.org/std/borrow/index.html)
[Cow in std::borrow - Rust](https://doc.rust-lang.org/std/borrow/enum.Cow.html)