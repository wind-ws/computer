


### MaybeUninit
可能没被初始化,延迟初始化

### ManuallyDrop
手动管理`Drop`
### drop
主动调用`Drop`

### forget
```rust
pub const fn forget<T>(t: T) {
	let _ = ManuallyDrop::new(t);
}
```
消耗(忘记)变量,且不调用`Drop`
### needs_drop
```rust
pub const fn needs_drop<T>() -> bool
where
    T: ?Sized,
```
检查类型`T`是否存在`Drop`, `true`存在`Drop`

注意: 若`T`未实现`Drop`,但`T`的字段实现了`Drop`,也表示`T`存在`Drop`

### transmute
```rust
pub const unsafe fn transmute<Src, Dst>(src: Src) -> Dst
```
将`Src`的内存数据 按位复制到`Dst`,且`forget(Src)`(不调用`Drop`)

需要保证`Src`和`Dst`的 内存大小和对齐 一致

### transmute_copy
```rust
pub const unsafe fn transmute_copy<Src, Dst>(src: &Src) -> Dst
```
按字节复制`Src`中的数据,到`Dst`中

源码中是调用`ptr::read`

### zeroed
```
pub const unsafe fn zeroed<T>() -> T
```
返回一个`T`,但`T`内部全由`0`填充

### replace

### swap

### take

### transmute

### transmute_copy

### discriminant
获取枚举的标识值
```rust
enum MyEnum {
    A,       // discriminant = 0
    B,       // discriminant = 1
    C = 42,  // discriminant = 42
    D,       // discriminant = 43
}
```
### size_of
```rust
pub const fn size_of<T>() -> usize
```
返回类型`T`占用的连续内存大小(包含 对齐填充大小)
即 结构`T`实际占用的连续内存大小
### size_of_val
```rust
pub const fn size_of_val<T>(val: &T) -> usize
where
    T: ?Sized,
```
与`size_of`不同的是,`size_of_val` 是动态获取结构`T`的大小,且可获取`?Sized`的大小

### align_of
查看结构最小内存对齐大小 (单位 字节)
### align_of_val
```rust
pub const fn align_of_val<T>(val: &T) -> usize
where
    T: ?Sized,
```
查看一个值的最小内存对齐大小 (单位 字节)

### offset_of!
**计算结构体中某个字段的偏移量（以字节为单位）**，即该字段相对于结构体开头的位置。


# 参考
[std::mem - Rust](https://doc.rust-lang.org/std/mem/index.html)
