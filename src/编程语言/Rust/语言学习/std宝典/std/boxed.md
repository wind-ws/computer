

### Box

```rust
Box<T> 与 Box<dyn Trait>的不同
在stack中 Box<T>只分配一个指向heap中的指针
而Box<dyn Trait>则分配 一个指向heap数据中的指针和一个 指向虚表的指针

另外,&dyn Trait 是在stack上分配 一个指向数据的指针 和 一个指向虚表的指针
与Box<dyn Trait>不同的是,&dyn Trait 是引用,而Box<dyn Trait>是拥有所有权
```

### ThinBox
#unsafe/self : 似乎是将[`Metadata`](https://rustwiki.org/zh-CN/std/ptr/trait.Pointee.html#associatedtype.Metadata "associated type std::ptr::Pointee::Metadata") 存储在 堆中,而非栈中, 栈中仅存储一个原始指针,指向堆空间



# 参考
[std::boxed - Rust](https://doc.rust-lang.org/std/boxed/index.html)
