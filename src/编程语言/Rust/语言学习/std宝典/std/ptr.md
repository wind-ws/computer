
### NonNull
非空原始指针

### addr_of!
在不创建临时引用（`&`）的情况下，从一个结构中获取其字段的原始指针

可使用语法`&raw const expr` 代替

### addr_of_mut!
相对于`addr_of!` ,就是获取一个可变的原始指针

可使用语法`&raw mut expr` 代替

### addr_eq
比较 **地址** 两个指针的 是否相等， 忽略胖指针中的任何元数据

### eq
比较**原始指针**是否相等

对于 胖指针 也会比较元数据

### fn_addr_eq
比较 两个函数指针的地址 是否相等 

在使用优化的情况下,可能(不保证) 不同位置声明的函数,但作用完全一样,地址会相同

### copy
```rust
pub const unsafe fn copy<T>(src: *const T, dst: *mut T, count: usize)
```

从`src` copy `count * size_of::<T>()`字节到 `dst` 
`src` 和`dst` 可能会重叠

### copy_nonoverlapping
与`copy`不同的是,`copy_nonoverlapping`不允许发生重叠

### dangling
返回 **指向对齐边界的地址，但永远不能被解引用** 的指针

一个占位指针

### dangling_mut
与`dangling`类似,只是返回的是 可变的原始指针

### drop_in_place
执行指向值的析构函数(T的Drop)

### from_mut
将可变引用转换为可变原始指针

相对于`r as *mut T` ,它更安全一些，因为它永远不会默默地改变类型或可变性，特别是 如果代码被重构

### from_ref
与`from_mut`类似,只是是处理 不可变的


### null
创建一个空原始指针
```rust
use std::ptr;

let p: *const i32 = ptr::null();
assert!(p.is_null());
assert_eq!(p as usize, 0); // this pointer has the address 0
```
### null_mut
创建一个可变空原始指针

### read
```rust
pub const unsafe fn read<T>(src: *const T) -> T
```
**从指针 `src` 所指向的位置**，**按字节复制出一份大小为 `size_of::<T>()` 的内存块**，然后 **作为 `T` 返回**
不会破坏`src`的数据
### read_unaligned
```rust
pub const unsafe fn read_unaligned<T>(src: *const T) -> T
```

`read`要求`src` 的地址必须满足 `T` 的对齐要求

`read_unaligned`**从一个可能没有对齐的指针 `src` 所指向的位置**，**按字节复制出一份大小为 `size_of::<T>()` 的内存块**，然后 **作为 `T` 返回**

### write
```rust
pub const unsafe fn write<T>(dst: *mut T, src: T)
```
将`src`按字节写入`dst`

注意: 不会调用`dst`的`Drop` , `dst`直接被掩盖

#unsafe : 对于`src`是`move`语义
### write_unaligned
与`write`不同的是,`write_unaligned`不要求内存对齐

### write_bytes
```rust
pub const unsafe fn write_bytes<T>(dst: *mut T, val: u8, count: usize)
```
`val`按一个字节将`T`写满, 写入`dst` ,一共写入`count * size_of::<T>()`大小的内存区域

```rust
use std::ptr;

let mut vec = vec![0u32; 4];
unsafe {
    let vec_ptr = vec.as_mut_ptr();
    ptr::write_bytes(vec_ptr, 0xfe, 2);
}
assert_eq!(vec, [0xfefefefe, 0xfefefefe, 0, 0]);
```

### replace
```rust
pub const unsafe fn replace<T>(dst: *mut T, src: T) -> T
```
将`src`的`T`移动到`dst`中, `dst`的`T`移动出来
二者都没被丢弃,仅仅是换一下位置,但触发了`move`语义

注意: `replace`是按字 节替换内存区域

### slice_from_raw_parts
根据原始指针和长度形成原始切片

### slice_from_raw_parts_mut
与`slice_from_raw_parts`不同的是,`slice_from_raw_parts_mut`返回的是可变的原始切片

### swap
```rust
pub const unsafe fn swap<T>(x: *mut T, y: *mut T)
```
通过`copy`实现的`swap`
按字节 交换 内存中的值

### swap_nonoverlapping
与`swap`不同的是,`swap_nonoverlapping`不允许发生重叠



# 参考
[std::ptr - Rust](https://doc.rust-lang.org/std/ptr/index.html)
