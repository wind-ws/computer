Sized 在编译期可以确定大小 (在栈区可确定分配内存大小)

DST 在编译期无法确定大小,只能在运行期确定大小


```rust
// ?Sized 表示 泛型T 可能是DST 也可能是确定大小的
fn generic<T: ?Sized>(t: &T) {
}
```
Sized 会默认修饰 泛型

