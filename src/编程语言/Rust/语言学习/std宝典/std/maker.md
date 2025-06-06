

### PhantomData
幽灵类型,用于标记结构,就像拥有了某些字段一样

### PhantomPinned
被标记的结构,不会实现`Unpin`


### Copy
实现后,具有Copy语义

### Send
实现后,可在线程发送所有权

允许不同线程传递所有权
### Sync
实现后,可在多线程中共享引用
允许多个线程拥有 一个存在的引用

### Unpin

# 参考
[std::marker - Rust](https://doc.rust-lang.org/std/marker/index.html)