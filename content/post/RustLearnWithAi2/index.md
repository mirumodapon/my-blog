---
date: '2025-04-22T22:42:36+08:00'
title: 用 AI 加速學習：Rust 基本語法與資料型態
image: cover.png
categories:
  - Rust 學習之旅
tags:
  - rust
---

## Rust 程式基本語法

首先我們來看看一段簡單的程式，這段程式會印出 Hello World！
```rust
fn main() {
    println!("Hello, World!");
}
```

其中：
- `fn` 是定義函數的關鍵字，`main` 是函數的名稱，也是整個程式的入口。
- `()` 是函數的參數，這裡是空的。  
- `{}` 是函數的內容，這裡是程式的主體。  
- `println!` 印出字串到終端（帶有 ! 表示它是一個宏 macro）。

這就是 Rust 的基本架構。

## Rust 的變數

### 變數的宣告

在 Rust 可以用 `let` 關鍵字來定義變數。
```rust
let x = 5;
```

這裡的 `x` 是變數的名稱，`5` 是變數的初始值。  
這裡的數值預設為 `i32`，也就是 32 位元整數。

我們也可以在變數宣告時指定變數的型態。
```rust
let y: i64 = 5;
```

如此一來 `y` 的型態就是 `i64`，也就是 64 位元整數。

接著，我們可以用 `println!` 來印出變數的值。
```rust
fn main() {
    let z = 12;
    println!("z = {}", z);
}
```

`println!` 的第一個參數是字串，
字串中 `"z = {}"` 使用了 `{}`，
這是佔位符（placeholder），表示要插入一個變數的值，
這個值會在接續的參數中被指定。

### 可變與不可變變數

在 Rust 中，變數的預設為不可變的（immutable），
當我們試圖改變變數的值時，會得到錯誤。
```rust
let x = 5;
x = 12; // ❌
```

如果我們想要改變變數的值時，
我們需要在變數宣告的時候，加上 `mut` 關鍵字。
```rust
let y = 12;
y = 5; // ⭕️
```

### 數值的表示方式

我們可以用以下方法來表示數值：
- 十進制數字： `12`, `-12`
- 十六進制數字： `0x6D`, `-0x4F`
- 八進制數字： `0o12`, `-0o12`
- 二進制數字： `0b1101`, `-0b1101`
- 浮點數： `12.5`, `-12.5`, `12.5e2`, `-12.5e2`
- 字元： `'a'`, `'中'`, `'😊'`
- 字串： `"Hello, World! 👋"`
- 布林值： `true`, `false`

這些數值都是可以在 Rust 中使用的。

## Rust 中的資料型態

### 基本資料型態

在 Rust 中，基本資料型態包括:

#### 整數（integer）
| 型別    | 描述                   |
| ------- | ---------------------- |
| `i8`    | 有符號 8 位元整數      |
| `i16`   | 有符號 16 位元整數     |
| `i32`   | 有符號 32 位元整數     |
| `i64`   | 有符號 64 位元整數     |
| `i128`  | 有符號 128 位元整數    |
| `isize` | 有符號系統依據的位元數 |
| `u8`    | 無符號 8 位元整數      |
| `u16`   | 無符號 16 位元整數     |
| `u32`   | 無符號 32 位元整數     |
| `u64`   | 無符號 64 位元整數     |
| `u128`  | 無符號 128 位元整數    |
| `usize` | 無符號系統依據的位元數 |

#### 浮點數（float）
| 型別    | 描述                   |
| ------- | ---------------------- |
| `f32`   | 32 位元浮點數          |
| `f64`   | 64 位元浮點數          |

#### 布林（boolean）
在 Rust 中，布林值以 `bool` 這個型別來表示，其值為 `true` 或 `false`。

#### 字元（character）
在 Rust 中，字元是一個 4 位元的 Unicode 字元。並且以 `char` 這個型別來表示字元。

### 複合資料型態

#### 元組（tuple）
元組是一組相同或不相同型別的值的集合。  
使用 小括號 `( )` 包住，並用逗號 `,` 分隔元素。  
Tuple 的長度是固定的，定義後無法改變。
```rust
let tuple: (i8, char, f32) = (1, '2', 3.0);
```

並且我們可以用解構賦值來讀取元組中的值。
```rust
let (x, y, z) = tuple;
```

如果想要讀取元組中的某一個值時，可以使用 `.`。
```rust
let x = tuple.0 // 第一個元素
let y = tuple.1 // 第二個元素
```

### 陣列（array）

陣列是固定長度的資料集合，其中每個元素都有相同的型別。  
陣列的大小在宣告時就必須確定，無法動態擴展。

```rust
fn main() {
    let numbers = [1, 2, 3, 4, 5];
}
```

我們也可以用 `[type; length]` 來宣告陣列：
```rust
fn main() {
    let numbers: [i32; 5] = [12; 5]
    // [12; 5] 等同於 [12, 12, 12, 12, 12]
}
```

在使用陣列時，與大部分的程式語言一樣，使用 `arr[index]` 來讀取陣列中的元素。
```rust
fn main() {
    let numbers = [12, 34, 56, 78, 90];
    let first = numbers[0];
    let last = numbers[4];

    println!("The first number is {}", numbers[0]);
    println!("The last number is {}", numbers[4]);
}
```

## 註解

在 Rust 中，可以使用 `//` 或是 `/* */` 來註解程式碼。
```rust
// 這是一個單行註解

/*
 * 這是一個多行註解
 */
```

## Rust 中的控制流程

### if 條件判斷

Rust 當中的 `if` 與大部分的程式語言的使用方式是類似的，  
當然也跟其他程式語言一樣，可以使用 `else if` 來增加條件判斷。  
比較嚴格的是條件判斷必須是 `bool` 型別。
```rust
fn main() {
    let age = 18;
    if age >= 18 {
        println!("You are an adult!");
    }
    else {
        println!("You are a child!");
    }
}
```


而在 Rust 當中，並沒有三元運算子，但我們可以使用 `if` 來達成相同的效果。  
值得注意的是，在 `if` 與 `else` 最後的內容不需要加上分號，而且必須是相同的型別。
```rust
fn main() {
    let age = 18;
    let message = if age >= 18 { "You are an adult!" } else { "You are a child!" };
    println!("{}", message);
}
```

並且我們也可以在 {} 當中，使用多個表達式。
```rust
fn main() {
    let x = 5;
    let y = if x > 0 {
        let z = 3;
        z * 2
    } else { -1 };

    println!("The value of y is {}", y); // 6
}
```

### match 條件判斷
`match` 類似於其程式語言中的 `switch`，用來對整數、字串、字元等值進行比對。

```rust
fn main() {
    let x = 1;
    match x {
        0 => println!("Hello"),
        1 => println!("World"),
        _ => println!("!"),
    }
}
```

在這段程式中，我們使用 `match` 來判斷 `x` 的值，並依照不同的值來執行不同的操作。  
其中 `_` 代表其他不符合上述條件的值。

`match` 也跟 `if` 一樣，回傳符合條件的數值。
```rust
fn main() {
    let x = 'A';
    let y = match x {
        'A' => 1,
        'B' => 2,
    }

    println!("{}", y); // 1
}
```

另外，`match` 可以多個條件合併，又或是在整數區間當中。
```rust
fn main() {
    let x = 3;
    let y = match x {
        1 | 2 => -1,
        4..=6 => 3, // 4 <= x <= 6
        7..8 => 4, // 7 <= x < 8
    };
}
```

### loop 迴圈

`loop` 是在 Rust 當中的無限循環迴圈，通常使用 `break` 或是配合 `return` 來跳出迴圈。

```rust
fn main() {
    let mut x = 0;
    loop {
        println!("Hello, World!");
        x += 1;

        if x > 10 {
            break;
        }
    }
}
```

### while 迴圈

`while` 與大部分程式語言行為相同，在符合條件下，持續執行迴圈內的程式。

```rust
fn main() {
    let mut x = 0;
    while x < 5 {
        println!("Hello, World!");
        x += 1;
    }
}
```

### for 迴圈

在 Rust 中，`for` 迴圈主要針對數組和迭代器進行迴圈運算。

```rust
fn main() {
    let arr = [1, 2, 3];
    for x in arr {
        println!("{}", x);
    }
}
```

要注意的是 `tuple` 是不能使用 `for` 迴圈的。

我們可以搭配 `.iter()` 與 `.enumerate()` 來使用迭代器。
```rust
fn main() {
    let arr = [1, 2, 3];
    for (index, x) in arr.iter().enumerate() {
        println!("{}: {}", index, x);
    }
}
```

如果要使用在字串當中，可以使用 `.chars()`。
```rust
fn main() {
    let s = "Hello, World!";
    for c in s.chars() {
        println!("{}", c);
    }
}
```

也可以在 `for` 迴圈中，使用連續整數
```rust
fn main() {
    for x in 0..10 {
        println!("{}", x);
    }

    for x in (0..=10).rev() {
        
    }
}
```

其中，`.rev()` 可以將其反轉。

### break 與 continue 迴圈控制

`beark` 可以用來跳出迴圈，`continue` 可以用來繼續下一次迴圈。

首先我們來看 `break`
```rust
fn main() {
    let mut x = 0;
    let mut sum = 0;
    loop {
        x += 1;
        if x % 2 == 0 {
            continue;
        }

        if x > 10 {
            break;
        }
    }
}
```

我們也可以幫迴圈標籤，並且在迴圈中指定要 `break` 或 `continue` 的迴圈。
```rust
fn main() {
    let mut x = 0;
    'outer: loop {
        x += 1;
        loop {
            x += 1;

            if x % 10 == 0 {
                continue 'outer;
            }
        }
    }
}
```

最後，我們來介紹 `break` 的回傳功能。
```rust
fn main() {
    let mut x = 0;
    let y = loop {
        x += 1;
        if x > 10 {
            break x
        }
    }
}
```

我們可以利用 `break` 來回傳數值，這裡跟 `match` 或是 `if` 一樣，回傳的數值後面不用加分號。

## 函式（Function）

在基本架構中，我們提到了程式的入口 `main`，就是一個函式，  
我們使用 `fn` 來定義函式。
```rust
fn say_hello() {
    println!("Hello, World!");
}
```

函式的參數、回傳值、呼叫函式等等，跟大部分程式語言的概念是一樣的，  
這裡就不再進一步介紹了。

比較值得注意的是我們可以在參數後方加上 `->` 來指定回傳值的型別。
```rust
fn add(x: i32, y: i32) -> i32 {
    return x + y;
}
```

並且在函式當中的最後一個陳述式，在不加上分號的情況下，會自動作為回傳值被回傳。
```rust
fn add(x: i32, y: i32) -> i32 {
    x + y
}

fn main() {
    println!("{}", add(1, 2)); // 3
}
```

## 陳述式與表達式

Rust 是基於表達式的語言（expression-based），因此在這個小節，我們要介紹的是陳述式和表達式的差別。

### 陳述式（Statements）

陳述式代表著程式當中的指令，這個指令不會回傳任何的數值。
像是：
```rust
let x = 12;
```

### 表達式（Expressions）

而表達式則是指程式當中的計算結果，這個計算結果會回傳一個數值。  
我們來看看這個範例：
```rust
fn main() {
    let x = {
        let a = 12;
        a << 1
    }

    println!("{}", x); // 24
}
```

這個範例中的 `{}`，如同函式的回傳一樣，就是表達式的一部分。

而其實在前幾個小節當中，我們已經看到了表達式，像是：
```rust
match x {
    ...
}
```

還有 `if` 條件判斷的表達式，這些可以產生一個數值的指令，也是表達式的一種。

---
<h4>參考資料</h4>

- [Rust Official Documentation Book, Section 3](https://doc.rust-lang.org/book/ch01-00-getting-started.html)
