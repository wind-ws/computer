
### 类型最大兼容性
> 若只需要某一个类型的功能,尽可能就只用这个类型,且保证可兼任其他类型
> 使用的类型是 最小需求集(即这个类型相比于其他类型 更加接近 刚刚好满足需求)
> 除非是需要性能优化

当你为函数选择参数类型时，使用带强制隐式转换的目标会增加你代码的复杂度。在这种情况下，函数将会接受更多的输入参数类型。

使用可切片类型或者胖指针类型没有限制。事实上，你应该总是用借用类型（**borrowed type**）, 而不是自有数据类型的借用（**borrowing the owned type**）。 例如`&str` 而非 `&String`, `&[T]` 而非 `&Vec<T>`, 或者 `&T` 而非 `&Box<T>`.

当自有数据结构（owned type）的实例已经提供了一个访问数据的间接层时，使用借用类型可以让你避免增加间接层。举例来说，`String`类型有一层间接层，所以`&String`将有两个间接层。我们可以用`&Str`来避免这种情况，无论何时调用函数，强制`&String`转换为`&Str`。

#### 参考
[以借用类型为参数 - Rust设计模式](https://chuxiuhong.com/chuxiuhong-rust-patterns-zh/idioms/coercion-arguments.html)


# 参考
[引言 - Rust设计模式](https://chuxiuhong.com/chuxiuhong-rust-patterns-zh/intro.html)
