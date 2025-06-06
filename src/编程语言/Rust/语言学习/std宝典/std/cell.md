可共享的可变的包装结构
实现结构内部可变性
可对一个不可变结构实现 字段可变性


### Cell\<T\>

[`Cell<T>`](https://rustwiki.org/zh-CN/std/cell/struct.Cell.html "struct std::cell::Cell") 通过将值移入和移出 cell 来实现内部可变性。 也就是说，永远无法获取到内部值的 `&mut T`，如果不将其替换为其他内容，则无法直接获取值本身。 这两条规则都确保永远不会有一个以上的引用指向内部值。

- 对于实现 [`Copy`](https://rustwiki.org/zh-CN/std/marker/trait.Copy.html "trait std::marker::Copy") 的类型，[`get`](https://rustwiki.org/zh-CN/std/cell/struct.Cell.html#method.get "method std::cell::Cell::get") 方法通过复制它来检索当前内部值。
- 对于实现 [`Default`](https://rustwiki.org/zh-CN/std/default/trait.Default.html "trait std::default::Default") 的类型，[`take`](https://rustwiki.org/zh-CN/std/cell/struct.Cell.html#method.take "method std::cell::Cell::take") 方法将当前内部值替换为 [`Default::default()`](https://rustwiki.org/zh-CN/std/default/trait.Default.html#tymethod.default "associated function std::default::Default::default")，然后返回替换后的值。
- 所有类型都有:
    - [`replace`](https://rustwiki.org/zh-CN/std/cell/struct.Cell.html#method.replace "method std::cell::Cell::replace"): 替换当前内部值并返回替换后的值。
    - [`into_inner`](https://rustwiki.org/zh-CN/std/cell/struct.Cell.html#method.into_inner "method std::cell::Cell::into_inner"): 此方法使用 `Cell<T>` 并返回内部值。
    - [`set`](https://rustwiki.org/zh-CN/std/cell/struct.Cell.html#method.set "method std::cell::Cell::set"): 该方法替换内部值，丢弃替换后的值。

### RefCell\<T>
`RefCell<T>` 的引用在运行时被跟踪

可以使用 [`borrow`](https://rustwiki.org/zh-CN/std/cell/struct.RefCell.html#method.borrow "method std::cell::RefCell::borrow") 获取对 `RefCell` 的内部值 (`&T`) 的不可更改引用，使用 [`borrow_mut`](https://rustwiki.org/zh-CN/std/cell/struct.RefCell.html#method.borrow_mut "method std::cell::RefCell::borrow_mut") 可以获取不可更改引用 (`&mut T`)。 当调用这些函数时，它们首先验证是否满足 Rust 的借用规则: 允许任意数量的不可改变借用或允许单个不可改变借用，但绝不能同时使用。 如果尝试违反这些规则的借用，线程将崩溃。

即运行时维护 包装字段的 可变性规则
### OnceCell\<T>
[`OnceCell<T>`](https://rustwiki.org/zh-CN/std/cell/struct.OnceCell.html "struct std::cell::OnceCell") 在某种程度上是 `Cell` 和 `RefCell` 的混合体，适用于通常只需要设置一次的值。 这意味着无需移动或复制内部值 (与 `Cell` 不同) 也无需运行时检查 (与 `RefCell` 不同) 即可获得引用 `&T`。 然而，它的值一旦设置也不能更新，除非您有一个可变引用到 `OnceCell`。

- [`get`](https://rustwiki.org/zh-CN/std/cell/struct.OnceCell.html#method.get "method std::cell::OnceCell::get"): 获取对内部值的引用
- [`set`](https://rustwiki.org/zh-CN/std/cell/struct.OnceCell.html#method.set "method std::cell::OnceCell::set"): 如果未设置则设置内部值 (返回 `Result`)
- [`get_or_init`](https://rustwiki.org/zh-CN/std/cell/struct.OnceCell.html#method.get_or_init "method std::cell::OnceCell::get_or_init"): 返回内部值，如果需要则初始化它
- [`get_mut`](https://rustwiki.org/zh-CN/std/cell/struct.OnceCell.html#method.get_mut "method std::cell::OnceCell::get_mut"): 提供对内部值的可变引用，仅当您对 cell 本身具有可变引用时才可用。

即允许第一次在不可变下 赋值, 后续的修改 都需要可变性

### LazyCell\<T>
在首次访问时初始化的值

### UnsafeCell\<T>


### SyncUnsafeCell\<T>
实现了`Sync`的`UnsafeCell`


# 参考
[std::cell - Rust](https://doc.rust-lang.org/std/cell/index.html)
