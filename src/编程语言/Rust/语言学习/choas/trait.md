
### 关联的项目
trait作为组合式抽象 服务于 结构, 关联的项目则作为抽象附带的存在

目前项目包括: 函数,类型,常量
函数 用于赋予结构 行为(能力)
类型 用于声明结构 与其他结构的关系
常量 用于赋予结构 附带的常量信息

> 结构本身是意义化(工具化)的存在, trait更多的是提供结构与结构之间的共识

### trait 自动解引用规则
优先搜索 Self类型 实现的函数,若搜不到,则进行解引用后 搜索 &Self类型
不止是解应用,还会自动 加引用
最短操作原则, 若解引用次数大于加引用,则优先进行加引用匹配函数

#unsafe : 在trait函数调用中的 自动类型判断 , 是优先判断 trait函数调用,再确定实际类型

#### example 
```rust
struct X { val: i32 }
impl std::ops::Deref for X {
    type Target = i32;
    fn deref(&self) -> &i32 { &self.val }
}

trait M { fn m(self); }
impl M for i32   { fn m(self) { println!("i32::m()");  } }
impl M for X     { fn m(self) { println!("X::m()");    } }
impl M for &X    { fn m(self) { println!("&X::m()");   } }
impl M for &&X   { fn m(self) { println!("&&X::m()");  } }
impl M for &&&X  { fn m(self) { println!("&&&X::m()"); } }

trait RefM { fn refm(&self); }
impl RefM for i32  { fn refm(&self) { println!("i32::refm()");  } }
impl RefM for X    { fn refm(&self) { println!("X::refm()");    } }
impl RefM for &X   { fn refm(&self) { println!("&X::refm()");   } }
impl RefM for &&X  { fn refm(&self) { println!("&&X::refm()");  } }
impl RefM for &&&X { fn refm(&self) { println!("&&&X::refm()"); } }


struct Y { val: i32 }
impl std::ops::Deref for Y {
    type Target = i32;
    fn deref(&self) -> &i32 { &self.val }
}

struct Z { val: Y }
impl std::ops::Deref for Z {
    type Target = Y;
    fn deref(&self) -> &Y { &self.val }
}


#[derive(Clone, Copy)]
struct A;

impl M for    A { fn m(self) { println!("A::m()");    } }
impl M for &&&A { fn m(self) { println!("&&&A::m()"); } }

impl RefM for    A { fn refm(&self) { println!("A::refm()");    } }
impl RefM for &&&A { fn refm(&self) { println!("&&&A::refm()"); } }


fn main() {
    // I'll use @ to denote left side of the dot operator
    (*X{val:42}).m();        // i32::m()    , Self == @
    X{val:42}.m();           // X::m()      , Self == @
    (&X{val:42}).m();        // &X::m()     , Self == @
    (&&X{val:42}).m();       // &&X::m()    , Self == @
    (&&&X{val:42}).m();      // &&&X:m()    , Self == @
    (&&&&X{val:42}).m();     // &&&X::m()   , Self == *@
    (&&&&&X{val:42}).m();    // &&&X::m()   , Self == **@
    println!("-------------------------");

    (*X{val:42}).refm();     // i32::refm() , Self == @
    X{val:42}.refm();        // X::refm()   , Self == @
    (&X{val:42}).refm();     // X::refm()   , Self == *@
    (&&X{val:42}).refm();    // &X::refm()  , Self == *@
    (&&&X{val:42}).refm();   // &&X::refm() , Self == *@
    (&&&&X{val:42}).refm();  // &&&X::refm(), Self == *@
    (&&&&&X{val:42}).refm(); // &&&X::refm(), Self == **@
    println!("-------------------------");

    Y{val:42}.refm();        // i32::refm() , Self == *@
    Z{val:Y{val:42}}.refm(); // i32::refm() , Self == **@
    println!("-------------------------");

    A.m();                   // A::m()      , Self == @
    // without the Copy trait, (&A).m() would be a compilation error:
    // cannot move out of borrowed content
    (&A).m();                // A::m()      , Self == *@
    (&&A).m();               // &&&A::m()   , Self == &@
    (&&&A).m();              // &&&A::m()   , Self == @
    A.refm();                // A::refm()   , Self == @
    (&A).refm();             // A::refm()   , Self == *@
    (&&A).refm();            // A::refm()   , Self == **@
    (&&&A).refm();           // &&&A::refm(), Self == @
}
```

#### reference 
[reference - What are Rust's exact auto-dereferencing rules? - Stack Overflow](https://stackoverflow.com/questions/28519997/what-are-rusts-exact-auto-dereferencing-rules/28552082#28552082)
