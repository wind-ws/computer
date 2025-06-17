


### Poll

### Context
调用`Future::poll`需要的一个参数

其作用是注册`Waker`供`poll`内部使用

若开启这个非稳定特性,则可通过`Context`向`poll`内部传递自定义数据
```rust
#[unstable(feature = "context_ext", issue = "123392")]
```
这是自定义数据的类型
```rust
#[derive(Debug)]
enum ExtData<'a> {
    Some(&'a mut dyn Any),
    None(()),
}
```

### Waker
`RawWaker`的封装结构

用于唤醒`Future`的执行 (一般言 是通知 指定的执行器去调度`Future`放入工作线程中执行)

### RawWaker
包含两个指针,一个指向Waker数据,一个指向Waker虚表(RawWakerVTable)
### RawWakerVTable
Waker的虚表结构



# 参考
[std::task - Rust](https://doc.rust-lang.org/std/task/index.html)
