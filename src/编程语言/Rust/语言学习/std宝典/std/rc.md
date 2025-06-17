

### Rc
单线程引用计数指针
提供 多所有者 使用 同一个内存区域 

`Rc`要求 strong== 1 时才可变
,**只要有多个所有者，就不能安全地进行可变操作**
,若没有这个限制,出现一块代码使用unsafe释放了指向的值,但其他所有者不知道,使用了被释放的值,就会导致安全问题


### Weak
单线程弱引用计数指针

它不一定能获取到值
,若所有strong 引用都被消耗后,Weak便无法获取值
,只有当所有strong和weak 引用都被消耗后,值才会drop


# 参考
[std::rc - Rust](https://doc.rust-lang.org/std/rc/index.html)
