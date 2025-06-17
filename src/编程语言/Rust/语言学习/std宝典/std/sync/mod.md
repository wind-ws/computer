


### Arc
多线程安全的引用计数指针

结构上 与`Rc`不同的是,`Arc`内部的strong和weak使用的是原子类型

`Arc`要求 strong== 1 时才可变
,**只要有多个所有者，就不能安全地进行可变操作**
,若没有这个限制,出现 一块代码或其他现场 使用unsafe释放了指向的值,但其他所有者不知道,使用了被释放的值,就会导致安全问题
### Weak
`Arc`的弱引用

### Barrier
使用`Barrier`可使多个线程能够同步开始 一些计算

若其他线程执行到`Barrier::wait`,必须等待所有线程中的`Barrier::wait`被调用

### BarrierWaitResult
`Barrier::wait`的返回值

### Condvar
可用于堵塞当前线程 并且将锁释放, 直到其他线程通知后,解除堵塞 唤醒现场,且重新获取锁

可能发生 虚假唤醒, 需标记一个状态来确保是真实唤醒
### WaitTimeoutResult

### LazyLock
第一次访问时初始化的值

此类型是线程安全的 `LazyCell`

### RwLock
读写锁

### RwLockReadGuard
`RwLock`的read锁`RAII`守卫

### RwLockWriteGuard
`RwLock`的write锁`RAII`守卫


### Mutex
互斥锁

### MutexGuard
`Mutex`的RAII守卫
用于访问锁住的值和自动释放锁

### PoisonError
中毒Rust中独有的多线程概念

若在 获取锁后 且 锁未释放 时 发生`panic` ,则会让锁中毒

检测是否中毒的函数
```rust
#[inline]
#[cfg(panic = "unwind")]
pub fn done(&self, guard: &Guard) {
	if !guard.panicking && thread::panicking() {
		self.failed.store(true, Ordering::Relaxed);
	}
}
```

### Once
用于一次性全局执行的低级同步原语

`Once`考虑中毒情况

`Once`的3个状态
```rust
pub(crate) enum ExclusiveState {
Incomplete,
Poisoned,
Complete,
}
```

在`Complete`状态下,说明 已经完成第一次执行,后续一切执行都无效(不会调用)
在`Poisoned`状态下,说明 之前调用`call_once`发生了中毒, 且 在中毒状态下,后续的`call_once`调用会直接`panic`即中毒
,在中毒下,调用`call_once_force`会忽略中毒,执行任务
,`call_once_force` 发生`panic`也会将状态变为`Poisoned`

### OnceLock
是线程安全的 [[src/编程语言/Rust/语言学习/std宝典/std/cell#OnceCell <T>|OnceCell <T>]]






# 参考
[std::sync - Rust](https://doc.rust-lang.org/std/sync/index.html)
