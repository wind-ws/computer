
### with C


#### crate
[Site Unreachable](https://crates.io/crates/libc)

### with C++

#### 注意事项
ffi交互 中 时刻注意 引用和指针 的影响

c++的对象,都要在c++内部进行创建和销毁,通过ffi与rust交互
除非清楚的知道结构的内部布局

Rust使用C++对象时, C++应该暴露 创建和销毁的函数,提供给Rust
,由Rust来 通过生命周期管理C++对象 (实现一个包装C++对象,实现Drop即可)

Rust提供给C++对象时,应该注意 生命周期的自动释放,应该给C++暴露 创建和销毁的函数

##### panic unwind
**Rust 和 C++ 的异常处理机制是不同的**，如果不正确处理，会导致 **未定义行为（UB）**，甚至是内存破坏、程序崩溃

- C++ 的异常系统通过 `throw` 抛出异常，通过 `catch` 捕获。
- 抛出异常时，C++ 会“展开栈”（stack unwinding）：逐层调用析构函数，直到遇到匹配的 `catch`。

- Rust 没有语言级别的异常系统，`panic!` 是一种“程序错误”的信号。
- 默认处理方式是 `unwind`（逐层调用 `Drop`，释放资源），或者可以配置为 `abort`（直接终止）。

#unsafe : 若使用"C-unwind"则可以让Rust和C++互相捕获panic


[外部函数接口（FFI） - Rust 秘典（死灵书）](https://nomicon.purewhite.io/ffi.html#ffi-%E5%92%8C-unwinding)
##### 0大小
注意 Rust中的0大小类型
C/C++没有0大小,若没有任何字段,一般是void的大小

#### crate
[Site Unreachable](https://crates.io/crates/cxx)

### with Python


