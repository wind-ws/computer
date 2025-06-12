

### \#\[repr(transparent)\]


#### 参考
[可选的数据布局 - Rust 秘典（死灵书）](https://nomicon.purewhite.io/other-reprs.html#reprtransparent)

### \#\[non_exhaustive]
表示`struct`或`enum` 将来可能会增加更多字段或变体

可用于 `struct` , `enum` 和 `enum`的字段 上 

#### 参考
[Type System - The Rust Reference](https://doc.rust-lang.org/reference/attributes/type_system.html#the-non_exhaustive-attribute)


### \#\[panic_handler]
在`no_std`中标记函数 用于处理`panic`

可用于`fn`
#### 参考
[#\[panic\_handler\] - The Rustonomicon](https://doc.rust-lang.org/nomicon/panic-handler.html)


### \#\[inline]

```rust
// 同时实现 inline 和 非inline 的函数
fn abc(){
	inline_abc()
}

#[inline]
fn inline_abc(){
...
}
```

### \#\[cold]

### \#\[no_builtins]
### \#\[target_feature]
### \#\[track_caller]

### \#\[instruction_set]
### \#\[recursion_limit]
### \#\[debugger_visualizer]
### \#\[collapse_debuginfo]


### \#\[global_allocator]

#### 参考
[std::alloc - Rust](https://doc.rust-lang.org/std/alloc/index.html#the-global_allocator-attribute)

## Perf


## Lint
用于控制或生成诊断 编译期间的消息

### \#\[allow]
### \#\[expect]
### \#\[warn]
### \#\[deny]
### \#\[forbid]

### \#\[deprecated]
弃用

### \#\[must_use]
### \#\[diagnostic]
### \#\[diagnostic::on_unimplemented]
### \#\[diagnostic::do_not_recommend]



## Derive
### \#\[derive]
### \#\[automatically_derived]

## Test
### \#\[test]

### \#\[ignore]

### \#\[should_panic]


# 参考
[Attributes - The Rust Reference](https://doc.rust-lang.org/reference/attributes.html)

