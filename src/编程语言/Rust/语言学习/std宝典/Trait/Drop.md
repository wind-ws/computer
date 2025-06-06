

### Drop 时机
当字段被修改时,若存在Drop,则Drop会被调用,后字段内存被新值覆盖
> 包括 变量(其他结构) 也是如此, 移动语义发生则调用Drop

### other
Drop和Copy不能同时实现

#### `Copy` and `Drop` are exclusive

You cannot implement both [`Copy`](https://doc.rust-lang.org/std/marker/trait.Copy.html "trait std::marker::Copy") and `Drop` on the same type. Types that are `Copy` get implicitly duplicated by the compiler, making it very hard to predict when, and how often destructors will be executed. As such, these types cannot have destructors.

注意Copy实现了(所以Drop不能为以下类型实现):
```rust
/// Shared references can be copied, but mutable references _cannot_!
#[stable(feature = "rust1", since = "1.0.0")]
impl<T: ?Sized> Copy for &T {}

marker_impls! {
    #[stable(feature = "rust1", since = "1.0.0")]
    Copy for
        usize, u8, u16, u32, u64, u128,
        isize, i8, i16, i32, i64, i128,
        f16, f32, f64, f128,
        bool, char,
        {T: ?Sized} *const T,
        {T: ?Sized} *mut T,

}
```
