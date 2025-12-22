- 每条指令周期数 (CPI) - 平均执行一条指令所需的周期数。
- 每周期指令数 (IPC) - 平均每个周期完成的指令数。

$$IPC= ​​INST\_RETIRED.ANY / ​CPU\_CLK\_UNHALTED.THREAD$$
$$CPI = 1/IPC$$
其中，`INST_RETIRED.ANY` 计算已完成指令的数量，`CPU_CLK_UNHALTED.THREAD` 计算线程不在中止状态时的核心周期数。


Linux `perf` 用户可以通过运行以下命令测量其工作负载的 IPC：
```
$ perf stat -e cycles,instructions -- a.exe
2369632 cycles
1725916 instructions # 0,73 insn per cycle
# 或更简单地:
$ perf stat ./a.exe
```