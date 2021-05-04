- [Rust的Pin与Unpin](https://folyd.com/blog/rust-pin-unpin/)
- [Pin UnPin 学习笔记](https://rustcc.cn/article?id=1d0a46fa-da56-40ae-bb4e-fe1b85f68751)


0. 什么是自引用结构体  
	safe rust 是无法创建的
1. 异步函数 生成器函数 基本都会用自引用结构体  
	rust compiler 生成
2. 自引用结构体 move swap replace 等操作会导致错误
3. 一个指针比如 Box<T> 能拿到 &mut T 就必然能做2  
```
	let t:T = 3
	let rmt = &mut t;
	let bt:Box<T> = Box::new(4);
	let rmbt = * &mut bt;
```
4. Pin 是指针 实现 Deref 一般用作 Pin<P<T>>  
	Pin<P<T>> where P:Unpin 可以拿到 &mut T  
	Pin<P<T>> where P:!Unpin 保证拿不到 &mut T  
5. 绝大部分类型都是 Unpin 自动实现
6. 实现 !Unpin  
默认 !Unpin 的  
	- PhantomPinned 给程序员用
	- async 块 编译器生成
	- 生成器函数 编译器生成  
给自己手动impl !Unpin  
struct 内包括 !Unpin 就是 !Unpin  
