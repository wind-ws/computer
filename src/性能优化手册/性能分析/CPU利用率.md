

CPU利用率是在一段时间内CPU处于忙碌状态的百分比。从技术上讲，当CPU不运行内核的`idle`线程时，CPU被认为是被利用的。


Linux `perf`会自动计算系统上所有CPU的CPU利用率：
```
$ perf stat -- a.exe
  0.634874  task-clock (msec) #    0.773 CPUs utilized
```
# 参考
[4-2.CPU利用率 · 现代CPU上的性能分析与优化](https://weedge.github.io/perf-book-cn/zh/chapters/4-Terminology-And-Metrics/4-2_CPU_Utilization_cn.html)