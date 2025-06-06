
### unreachable_unchecked
不可达代码部分 的优化

`unreachable!`可能阻止一些优化,若可保证一定不可达,则使用`unreachable_unchecked`进行优化

# 参考
[std::hint - Rust](https://doc.rust-lang.org/std/hint/index.html)
