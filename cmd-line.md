# 链接
- [命令行库](https://lib.rs/command-line-interface)

# args 参数处理
- [std::env::args()](https://doc.rust-lang.org/std/env/fn.args.html) 内置
- [crates::getopts](https://crates.io/crates/getopts) 半官方 简单
- [crates::clap](https://crates.io/crates/clap) 最多使用 生成帮助 复杂
- [crates::structopt](https://crates.io/crates/structopt) 基于 clap 简化

# env 环境变量
[std::env](https://doc.rust-lang.org/std/env/index.html)
- vars/var/set_var 处理环境变量
- current_exe 当前程序
- current_dir/set_current_dir 当前目录
- temp_dir 临时目录
- home_dir 家目录 不推荐 Deprecated
- split_paths/join_paths `PATH` 变量处理
```rust
use std::env;
use std::path::PathBuf;

fn main() -> Result<(), env::JoinPathsError> {
    if let Some(path) = env::var_os("PATH") {
        let mut paths = env::split_paths(&path).collect::<Vec<_>>();
        paths.push(PathBuf::from("/home/xyz/bin"));
        let new_path = env::join_paths(paths)?;
        env::set_var("PATH", &new_path);
    }

    Ok(())
}
```

# 输入输出
- [crates::colored](https://crates.io/crates/colored) 输出多色
- [crates::repl-rs](https://crates.io/crates/repl-rs) shell 式界面
- [rust版的console进度条实现](https://rustcc.cn/article?id=dd902f80-1399-402d-b6cd-37a96fe39f36)
- [密码回显(C&Unix)](https://www.zhihu.com/question/460815274/answer/1901053384)

# pipe
