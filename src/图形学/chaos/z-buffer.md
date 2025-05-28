

所谓z-buffer 就是判断这个点是否应该被渲染
那是在xy轴重复的点,通过获取z值来判断 这个点是否在另一个点前面
所以z-buffer有称为 深度缓冲
获取点的深度,判断点是否被渲染

# 参考
[深度缓冲 - 维基百科，自由的百科全书](https://zh.wikipedia.org/wiki/%E6%B7%B1%E5%BA%A6%E7%BC%93%E5%86%B2)
[计算机图形学 学习笔记（六）：消隐算法：Z-buffer，区间扫描线，Warnock，光栅图形学小结\_计算机图形学实验zbuffering消隐实现-CSDN博客](https://blog.csdn.net/Jurbo/article/details/75007260)
[day4：Z-buffering（深度缓冲） | 卤代烃实验室](https://supercodepower.com/docs/toy-renderer/day4-Z-buffering)
