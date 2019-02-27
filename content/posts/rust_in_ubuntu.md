+++
title = "一行搞定rust的运行环境"
date = "2015-12-30T21:13:25+08:00"
tags = []

+++


# rust运行环境的安装

## 安装

```bash
$ curl -sSf https://static.rust-lang.org/rustup.sh | sh
```

## helloworld

- 方法一:rustc
```rust
// save file as helloworld.rs
fn main() {
    println!("hello helab")
    }
```

```bash
$ rustc helloworld.rs
$ ./helloworld
```

- 方法二:cargo
```bash
$ cargo new rust_first_project --bin
$ cargo build
$ cargo run
```
