
Pin 它包裹一个指针，并且能确保该指针指向的数据不会被移动，例如 `Pin<&mut T>` , `Pin<&T>` , `Pin<Box<T>>` ，都能确保 `T` 不会被移动


- 若 `T: Unpin` ( Rust 类型的默认实现)，那么 `Pin<'a, T>` 跟 `&'a mut T` 完全相同，也就是 `Pin` 将没有任何效果, 该移动还是照常移动
- 绝大多数标准库类型都实现了 `Unpin` ，事实上，对于 Rust 中你能遇到的绝大多数类型，该结论依然成立 ，其中一个例外就是：`async/await` 生成的 `Future` 没有实现 `Unpin`
- 你可以通过以下方法为自己的类型添加 `!Unpin` 约束：
    - 使用文中提到的 `std::marker::PhantomPinned`
    - 使用`nightly` 版本下的 `feature flag`
- 可以将值固定到栈上，也可以固定到堆上
    - 将 `!Unpin` 值固定到栈上需要使用 `unsafe`
    - 将 `!Unpin` 值固定到堆上无需 `unsafe` ，可以通过 `Box::pin` 来简单的实现
- 当固定类型 `T: !Unpin` 时，你需要保证数据从被固定到被 drop 这段时期内，其内存不会变得非法或者被重用

#unsafe : 只有被Pin包装的数据,不可被移动,但数据任可移动
```rust
fn main() {
   let mut test1 = Test::new("test1");
   let mut test1_pin = unsafe { Pin::new_unchecked(&mut test1) };
   Test::init(test1_pin.as_mut());

   drop(test1_pin);
   println!(r#"test1.b points to "test1": {:?}..."#, test1.b);

   let mut test2 = Test::new("test2");
   mem::swap(&mut test1, &mut test2);
   println!("... and now it points nowhere: {:?}", test1.b);
}

```

但是，在实际应用中，一些函数会要求它们处理的 `Future` 是 `Unpin` 的，此时，若你使用的 `Future` 是 `!Unpin` 的，必须要使用以下的方法先将 `Future` 进行固定:

- `Box::pin`， 创建一个 `Pin<Box<T>>`
- `pin_utils::pin_mut!`， 创建一个 `Pin<&mut T>`

固定后获得的 `Pin<Box<T>>` 和 `Pin<&mut T>` 既可以用于 `Future` ，**又会自动实现 `Unpin`**。