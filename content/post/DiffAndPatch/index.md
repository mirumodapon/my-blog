---
date: '2025-08-23T22:17:33+08:00'
title: 用 Diff 與 Patch 精準傳遞檔案修改
image: cover.png
tags:
  - gnu
  - linux
  - diff
  - patch
---

最近在公司與公司的夥伴協作的時候，往往有需要傳遞一些檔案的修改方式，其實大多數在改動的時候都是直接用版本管理工具像是 `git` 或是 `svn`（沒錯先不要懷疑，在 2025 的今天，我們公司還在使用 `svn`），但在有些情境下，我們可能不想推到 git server 上（比如說敏感資料檔案不會被 `git` 追蹤）。

<!--

目前在公司夥伴的做法就是寫一封信，並且貼一小段修改的部分，然後把這些部分用顏色標記起來，然後他就改錯了。尤其是 `yaml` 這種需要縮排的檔案，在信件中如果沒有使用等寬字體，根本就看不出來需要空幾格。

-->

## GNU diffutils

接下來要先介紹 GNU diffutils，這是 GNU 發布的比較工具包。在有些 Linux 發行版當中已經預設安裝了，如果在你的發行版中沒有這個工具包。你可以利用你的套件管理工具安裝 `diffutils`：

ubuntu:
```bash
$ apt install diffutils
```

## `cmp`
cmp - compare two files byte by byte

`cmp` 會在發現第一個相異點之後停下來，並且回傳不一樣的地方資訊。
這個指令會透過位元組的方式比較兩個檔案，基本用法如下：

```bash
cmp file1 file2
# output:
# file1 file2 differ: byte 1, line 1
```

`-b`, `--print-bytes` 可以用來顯示不一樣的地方是什麼：
```bash
cmp -b file1 file2
# output:
# file1 file2 differ: byte 1, line 1 is 164 t 150 h
```

`-i`, `--ignore-initial=SKIP` 跳過 n 個 bytes 在進行比較：
```bash
# 從第 3 個 byte 開始比較 (跳過 2 個 bytes)
cmp -i 2 file1 file2
```

也可以分別設定兩個檔案要跳過的 bytes 數量：
```bash
# 第一個檔案從第 3 個 byte 開始比較 (跳過 2 個 bytes)
# 第二個檔案從第 4 個 byte 開始比較 (跳過 3 個 bytes)
cmp -i 2:3 file1 file2
```

這個指令大多用來比較兩個檔案是否完全相同。

## `diff`
 diff - compare files line by line

 這個指令最主要是要比較文本，他會比對兩個文本是否一致並且把不一樣的地方列出來。
 這邊我先準備兩個檔案來更好的解釋：
```bash
cat << EOF > file1.cpp
#include <iostream>

int main() {
    std::cout << "Hello World!" << std::endl;
    return 0
}
EOF

cat << EOF > file2.cpp
#include <iostream>
using namespace std;

int main() {
  cout << "Hello World!" << endl;
  return 0;
}
EOF
```

接著我們就可以用 `diff` 來比較差異了：

 ```bash
diff file1.cpp file2.cpp
# output:
# 1a2
# > using namespace std;
# 4,5c5,6
# <     std::cout << "Hello World!" << std::endl;
# <     return 0
# ---
# >   cout << "Hello World!" << endl;
# >   return 0;
```

<details>
	<summary>輸出說明</summary>

觀察輸出我們可以得到：

- `1a2`：
    - 前面的數字 `1` 表示 `file1.cpp` 的第一行
    - 後面的數字 `2` 表示 `file2.cpp` 的第二行
    - `a` 表示新增了一行

-  `4,5c5,6`:
  - 前面的 `4,5` 表示 `file1.cpp` 的第四行到第五行
  - 後面的 `5,6` 表示 `file2.cpp` 的第五行到第六行

表達完更改的地方之後，後面就是更改的內容啦！用 `<` 表示 `file1.cpp` 的檔案，`>` 則表示 `file2.cpp` 的檔案。
</details>

這樣你可能會覺得很複雜因此我們可以加入 `-u, -U NUM, --unified[=NUM]` 來用 git 風格的格式顯示：
```bash
diff -u file1.cpp file2.cpp
# output:
# --- file1.cpp   2026-02-08 19:35:32.593297916 +0800
# +++ file2.cpp   2026-02-08 19:35:32.596297778 +0800
# @@ -1,6 +1,7 @@
#  #include <iostream>
# +using namespace std;
#
#  int main() {
# -    std::cout << "Hello World!" << std::endl;
# -    return 0
# +  cout << "Hello World!" << endl;
# +  return 0;
#  }
```

<details>
	<summary>輸出說明</summary>
    
- 第一與第二行的 `---` 與 `+++` 分別表示 file1.cpp 與 file2.cpp。後面則為最後修改時間。
- `@@ -1,6 +1,7 @@`
    - `-1,6`：舊檔從第 1 行開始，共 6 行
    -  `+1,7`：新檔從第 1 行開始，共 7 行
</details>

## `sdiff`

 sdiff - side-by-side merge of file differences

 這個指令也是用來顯示兩個檔案不一樣的地方，最大的不同是他會以左右並排的方式呈現，這應該是人類最好閱讀的方式。

 ```bash
sdiff file1.cpp file2.cpp
```

## `patch`

這應該就是今天的重點了，我們利用完 `diff` 指令可以直接存成檔案：
```bash
diff file1 file2 > file.patch
```

這樣就可以把生成出來的檔案直接丟給同事，接著他只要用下方的指令，就可以直接把改動的部分直接更新到他的電腦：
```bash
patch file < file.path
```

這麼一來就不會有改錯檔案的問題啦！




---
<h4>延伸閱讀</h4>

- `git apply`
- `diff3`

---

<h4>參考資料</h4>

- [GNU Diffutils](https://www.gnu.org/software/diffutils/)

<style>
details {
    background: #66BBED;
    border-radius: 5px;
    margin: 5px 0;
    padding: 8px;
}

details code {
    color: #333 !important;
}
</style>
