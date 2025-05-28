
&'static 与 T: 'static

T: 'static 的意思是对T约束 拥有所有权 或者 不包含非'static生命周期的引用

`&'static` 对于生命周期有着非常强的要求：一个引用必须要活得跟剩下的程序一样久，才能被标注为 `&'static`

