
在系统中 开辟一块独立的内存区域 (并非在进程的堆栈中)
除非重启系统或主动释放,否则shm的内存区域一直存在.

可通过mmap将shm独立内存区域,映射到进程内存中


#unsafe/ai
在共享内存中的Atomic ,即使不是同一进程,也可以保证原子性.
因为原子操作是对指定内存区域的原子操作.
不同进程 指向的 仍是相同的内存区域,所以可以保证原子性


# 参考
[内存映射(mmap)和共享内存(shm) - Lin\_泠沐 - 博客园](https://www.cnblogs.com/cheer-lingmu/p/16443963.html)
[Site Unreachable](https://zhuanlan.zhihu.com/p/650723391)
