---
date: '2025-01-04T22:59:50+08:00'
title: Hello World
tags:
  - helloWorld
---

在資訊科技領域中，「Hello World」經常被用來作為測試開發環境是否正確設置的一種方式，透過將這段文字打印或顯示出來，開發者能迅速確認系統的基本運行狀態。因此我利用這篇文章，作為整個部落格的第一篇文。

## Hello World 的起源

「Hello World」這個程式的歷史可以追溯到 1970 年代。《The C Programming Language》（C 語言程式設計）這本經典書籍中，Brian Kernighan 和 Dennis Ritchie 使用了一個簡單的範例來介紹如何在螢幕上顯示文字，而這個範例就是「Hello, World!」。由於其簡單易懂且不容易出錯，它很快成為程式設計入門的標誌。

「Hello, World」的概念可以追溯到 Brian Kernighan 在 1974 年的內部技術手冊 《Programming in C: A Tutorial》，
他在該手冊中用 B 語言（C 語言的前身）展示了類似的範例程式碼：
```b
main() {
    printf("hello, world");
}
```

## Hugo 功能測試

### 一般標記

#### *斜體*
`*斜體*`

#### **粗體**
`**粗體**`

#### ~~刪除線~~
`~~刪除線~~`

#### ==標記==
`==標記==`

#### ++底線++
`++底線++`

#### 上^標^
`上^標^`

#### 下~標~
`下~標~`

### 程式碼


#### 一般顯示
```c
#define hugo
```

#### 程式碼標記

{{< highlight go "linenos=inline, hl_lines=3 6-8, style=emacs" >}}
package main

import "fmt"

func main() {
    for i := 0; i < 3; i++ {
        fmt.Println("Value of i:", i)
    }
}
{{< /highlight >}}


### Latex Math

\[
\begin{aligned}
KL(\hat{y} || y) &= \sum_{c=1}^{M}\hat{y}_c \log{\frac{\hat{y}_c}{y_c}} \\
JS(\hat{y} || y) &= \frac{1}{2}(KL(y||\frac{y+\hat{y}}{2}) + KL(\hat{y}||\frac{y+\hat{y}}{2}))
\end{aligned}
\]


This is an inline \(a^*=x-b^*\) equation.

{{< notice error >}}
{{< /notice >}}

{{< notice warning >}}
{{< /notice >}}

{{< notice success >}}
{{< /notice >}}

{{< notice info test >}}
{{< /notice >}}

---

<h4>參考資料</h4>

- [wikipedia - "Hello, World!" program](https://en.wikipedia.org/wiki/%22Hello,_World!%22_program)
