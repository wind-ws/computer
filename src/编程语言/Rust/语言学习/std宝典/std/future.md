

### Future


### 对于异步运行时实现的记录
大致模块是
1. 执行器: 负责执行Future poll
2. 反应器: 负责接受信号(例如 epoll),接受后让Future poll重新执行(一般在执行器中执行,一般反应器只调用Waker)
3. Future: 负责编写执行代码
4. Waker: 负责唤醒执行器,让执行器再次执行对应的Future poll

若需要更多特性,模块可以更加复杂

# 参考
[std::future - Rust](https://doc.rust-lang.org/std/future/index.html)