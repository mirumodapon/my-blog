---
date: '2025-03-29T22:58:27+08:00'
title: 用 AI 加速學習：Rust 語言簡介與環境設置
image: cover.png
categories:
  - Rust 學習之旅
tags:
  - rust
---

## Rust 是什麼？

Rust 是一個邊一行的程式語言，主打安全性、速度、並行處理。
相對於其他程式語言來說 Rust 可以說是非常年輕的，
2012 年 1 月懷上的它，直到 2015 年 5 月 15 日才出生。

## 安裝 Rust

在 Rust 個[官方網站](https://www.rust-lang.org/)中，
推薦了使用 rustup 來安裝 Rust。
rustup 是 Rust 官方提供的工具鏈安裝與管理器，
可以讓你方便地安裝 Rust、切換不同版本。
Unix-like 作業系統可以執行以下指令來安裝 rustup：
```bash
$ curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

接這我們就可以使用 `rustup` 指令來安裝 Rust。

```bash
$ rustup install stable
```

這個指令會幫我們下載 Rust 的穩定版本，與相關的工具（包含 rustfmt、cargo 等）。

## Hello Rust

安裝完之後，可以使用 `rustc --version` 指令來檢查是否安裝成功。
這是 Rust 的編譯器，可以用來編譯 Rust 程式。

接這我們就可以開始寫 Rust 程式了！
首先建立一個檔案 `hello.rs`，並在裡面寫入以下程式：
```rust
fn main() {
  println!("Hello, Rust!");
}
```

其中：
- `fn` 是建立函數的關鍵字。
- `main` 是函數的名稱，在 Rust 當中 main 作為整個程式的入口。
- `println!` 以 `!` 結尾在 Rust 中表示巨集（macro）。
- `"Hello, Rust!"` 是要印出的字串。

接著使用以下指令來編譯程式：
```bash
$ rustc hello.rs
```

這樣就可以編譯出一個與檔案名稱相同的執行檔了。
我們試著執行這個執行檔。
```bash
$ ./hello
Hello, Rust!
```

## Cargo

**Cargo** 是 Rust 的建置工具與套件管理工具，
大多數專案都會透過 Cargo 進行管理。  
透過 `rustup` 安裝 Rust 時，Cargo 也會一併安裝。

首現我們先用 Cargo 建立一個專案：
```bash
$ cargo new hello_cargo
```

這時 cargo 會幫我們建立一個結構如下的資料夾：
```
hello_cargo
├── .git
│   └── (...)
├── src
│   └── main.rs
├── Cargo.toml
└── .gitignore
```

其中，`main.rs` 是程式的入口，`Cargo.toml` 是專案的配置檔。

進入專案資料夾後，我們可以打開 `src/main.rs`，並且將剛剛的程式寫入這個檔案中。
接著透過 Cargo 指令來執行專案。Cargo 會自動編譯原始碼並執行可執行檔。
```bash
$ cargo run
   Compiling hello_rust v0.1.0 (/playground/hello_rust)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.17s
     Running `target/debug/hello_rust`
Hello, world!
```

這個指令執行直，會先編譯 `src/main.rs`，再執行程式。
這個編譯的結果，會生成在路徑 `target/debug/hello_rust` 當中。

我們也可以編譯但不執行檔案：
```bash
$ cargo build
```

或是僅檢查程式的語法錯誤，但不編譯該程式：
```bash
$ cargo check
```

最後，當我們完成了專案時，可以使用 release 模式進行最佳化編譯。  
```bash
$ cargo build --release
````
這會產生效能更好的執行檔，放在 `target/release` 目錄中。雖然編譯時間會增加，但執行效率會大幅提升。

---
<h4>參考資料</h4>

- [Rust Official Documentation Book, Section 1](https://doc.rust-lang.org/book/ch01-00-getting-started.html)
- [Rust in 100 Seconds](https://youtu.be/5C_HPTJg5ek)
