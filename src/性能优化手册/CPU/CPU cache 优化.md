


- **时间局部性**：当访问给定的内存位置时，很可能在不久的将来再次访问同一位置。理想情况下，我们希望在下一次需要时，该信息位于缓存中。
- **空间局部性**：当访问给定的内存位置时，很可能会在不久的将来访问附近的位置。这指的是将相关数据放在彼此附近。当程序从内存中读取一个字节时，通常会获取更大的内存块（缓存行），因为该程序很可能很快就会需要该数据。

### 基础概念

#### cache line
#### cache missing

#### 缓存一致性

#### MESI 协议

[MESI协议 - 维基百科，自由的百科全书](https://zh.wikipedia.org/wiki/MESI%E5%8D%8F%E8%AE%AE)
#### 伪共享(false sharing)

[伪共享（false sharing），并发编程无声的性能杀手 - cyfonly - 博客园](https://www.cnblogs.com/cyfonly/p/5800758.html)
[伪共享 - 维基百科，自由的百科全书](https://zh.wikipedia.org/wiki/%E4%BC%AA%E5%85%B1%E4%BA%AB)

# 参考
[CPU Cache Optimization — zzq's blog](https://zzqcn.github.io/perf/cpu_cache.html#cpu-cache-the-need-to-know)
[一篇论文讲透Cache优化](https://zhuanlan.zhihu.com/p/608663298)
