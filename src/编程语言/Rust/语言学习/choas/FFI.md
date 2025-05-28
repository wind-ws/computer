
### with C


#### crate
[Site Unreachable](https://crates.io/crates/libc)

### with C++

#### 注意事项
ffi交互 中 时刻注意 引用和指针 的影响

c++的对象,都要在c++内部进行创建和销毁,通过ffi与rust交互
除非清楚的知道结构的内部布局
##### 0大小
注意 Rust中的0大小类型
C/C++没有0大小,若没有任何字段,一般是void的大小

#### crate
[Site Unreachable](https://crates.io/crates/cxx)

### with Python


