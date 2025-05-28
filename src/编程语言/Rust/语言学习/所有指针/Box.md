

```rust
Box<T> 与 Box<dyn Trait>的不同
在stack中 Box<T>只分配一个指向heap中的指针
而Box<dyn Trait>则分配 一个指向heap数据中的指针和一个 指向虚表的指针

另外,&dyn Trait 是在stack上分配 一个指向数据的指针 和 一个指向虚表的指针
与Box<dyn Trait>不同的是,&dyn Trait 是引用,而Box<dyn Trait>是拥有所有权
```
