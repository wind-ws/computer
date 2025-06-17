

### Scope
#todo : 研究一下`Scope`的 变异性 

### spawn
创建一个线程,返回其句柄

### current
获取调用它的线程的句柄

### panicking
```rust
pub fn panicking() -> bool
```
true: 当前线程是 由于恐慌而解除

一般言 `panicking`在`Drop`中常用, 因发生`panic`后`unwind`调用`Drop`

### park
调用`park`可让当前线程 堵塞 (若提前调用了`Thread::unpark`则不会堵塞)

`Thread::unpark` 可解开堵塞
### park_timeout
与`park`不同的是,`park_timeout`可设置超时, 若超时自动解开堵塞

### scope
创建一个范围, 在范围内 可以创建多个 作用域线程

作用域线程可以借用非 `'static` 数据

保证在退出作用域前自动 join 所有线程,所以`scope`函数结束后 所有作用域线程都以结束

#todo : `scope`是如何处理`panic`的
### sleep
使当前线程休眠至少的指定时间


# 参考
[std::thread - Rust](https://doc.rust-lang.org/std/thread/index.html)
