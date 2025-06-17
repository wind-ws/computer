
async block 会生成为一个闭包,在 HIR级别可查看

异步代码的状态机 生成在MIR级别, 想要看具体生成的是什么,需要通过编译到MIR查看

### `Future` 的匿名类型


#unsafe #todo : 暂时未写完,待确认一些信息(实际生成 远远比下面的 要复杂!!! 下面只是给个简单的例子(但不正确))
```rust
let fut_one = /* ... */; // Future 1
let fut_two = /* ... */; // Future 2
async move {
	a();
    fut_one.await;
    b();
    fut_two.await;
	c();
}
```
在底层，`async` 会创建一个实现了 `Future` 的匿名类型，并提供了一个 `poll` 方法：
```rust
// `async { ... }`语句块创建的 `Future` 类型
struct AsyncFuture {
    fut_one: FutOne,
    fut_two: FutTwo,
    state: State,
}

// `async` 语句块可能处于的状态
enum State {
	Start,
    AwaitingFutOne,
    AwaitingFutTwo,
    Done,
}

impl Future for AsyncFuture {
    type Output = ();

    fn poll(mut self: Pin<&mut Self>, cx: &mut Context<'_>) -> Poll<()> {
        loop {
            match self.state {
	            State::Start => {
		            a();
		            match self.fut_one.poll(..) {
	                    Poll::Ready(()) => self.state = State::AwaitingFutTwo,
	                    Poll::Pending => {
				            self.state = State::AwaitingFutOne;
							return Poll::Pending
		                },
	                }
	            }
                State::AwaitingFutOne => match self.fut_one.poll(..) {
                    Poll::Ready(()) => self.state = State::AwaitingFutTwo,
                    Poll::Pending => return Poll::Pending,
                }
                State::AwaitingFutTwo => match self.fut_two.poll(..) {
                    Poll::Ready(()) => self.state = State::Done,
                    Poll::Pending => return Poll::Pending,
                }
                State::Done => return Poll::Ready(()),
            }
        }
    }
}

```

另一个例子:
```rust
async {
    let mut x = [0; 128];
    let read_into_buf_fut = read_into_buf(&mut x);
    read_into_buf_fut.await;
    println!("{:?}", x);
}
```

```rust
struct ReadIntoBuf<'a> {
    buf: &'a mut [u8], // 指向下面的`x`字段
}

struct AsyncFuture {
    x: [u8; 128],
    read_into_buf_fut: ReadIntoBuf<'what_lifetime?>,
}
```


# 参考
[lowering async await in rust - wiki](https://wiki.cont.run/lowering-async-await-in-rust/)
