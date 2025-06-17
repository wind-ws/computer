
### unreachable_unchecked
告诉编译器 这处代码一定不可达,编译器会做出

不可达代码部分 的优化

`unreachable!`可能阻止一些优化,若可保证一定不可达,则使用`unreachable_unchecked`进行优化

### assert_unchecked
```
pub const unsafe fn assert_unchecked(cond: bool)
```
告诉编译器 `cond`这段表达式 总是返回`true` ,然后交给编译器优化后续的代码

注意: 若不返回`true`则会发生`UB`,因为代码已经优化了(优化删除了一些 在`true`情况下 无用的代码,例如分支)

在使用`assert_unchecked`时,建议在下面加一个`debug_assert!` 确保`cond`为`true` (`debug`下保证安全)

# 参考
[std::hint - Rust](https://doc.rust-lang.org/std/hint/index.html)
