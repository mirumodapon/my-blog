---
date: '2025-02-23T13:22:01+08:00'
draft: true
title: 用對 Mac 工具，連貓都能寫程式
image: cover.png
tags:
  - tools
---

最近在逛 Apple 官網的時候，看到了 2 萬多塊 的 MacBook Air M2 整修品，
剛好我也快要受不了女朋友的電腦了，索性就下單了 ~~

不過她是第一次用 Mac，於是我就先來幫她設定啦，
順便分享一下我常使用的 Mac 工具。

## 終端機

### iTerm2

身為一個軟體工程師（她應該之後也會是吧？！），終端機是我們很重要的工具。
[**iTerm2**](https://iterm2.com/) 是一個終端機模擬器（Terminal emulator），可以當作是macOS 上的**強化版終端機**，
提供比內建終端更強大的功能、客製化選項與提升生產力的特性，很適合開發者、系統管理員及資深使用者使用。

### tmux

[**tmux**](https://github.com/tmux/tmux/wiki)（Terminal Multiplexer）是一款終端多工管理工具，
允許你在單一終端會話（Session）中管理多個視窗與面板，
並支援背景運行、遠端連線保持、分割視窗等功能。

## 整合開發環境（IDE)

### Neovim

[**Neovim**](https://neovim.io/) 是 Vim 的改進版，目標是現代化、可擴充、提升效能，
並提供更友善的插件開發與 Lua 配置。
相較於傳統 Vim，Neovim 在 外掛系統、LSP（Language Server Protocol）、內建終端、多執行緒處理等方面有更好的支援，
使其成為現代開發者的首選終端編輯器。

雖然這東西對初學的人來說很不友善，但她在 VSCode 裡也都用 Vim 模式，應該也沒什麼問題（吧？！）

### Cursor

[**Cursor**](https://www.cursor.com/) 是由 VSCode Fork 出來的 IDE，它提供了生成式 AI 來幫助開發者寫程式。
只要打上需求，就自動寫出你要的功能，上班按按 `Tab` 就可以下班了 XD

### Zed

[**Zed**](https://zed.dev/) 是一款由 Rust 開發的 IDE，比起 VSCode 速度可是快了非常的多。
它的一大亮點是它的即時協作功能，使得團隊中的多位開發者可以同時在同一個代碼庫中進行編輯。
同時也整合了 LLM 提供開發的協助。

## Markdown 編輯器

<small>這個部分最主要是作為筆記用的工具，而我對筆記工具沒什麼要求，支援 Markdown 輸出就行。</small>

### Zettlr

作為開源的推廣者，[**Zettlr**](https://www.zettlr.com/) 是我非常喜歡的一款開源 Markdown 編輯器，
畫面乾淨、簡單又容易上手。並且內建對 LaTeX、HTML 等格式的良好支援，
使其成為學術寫作、技術寫作、程式碼文檔等領域的理想選擇。

### Obsidian

[**Obsidian**](https://obsidian.md/) 是一款強大的知識管理和筆記整理工具，
可以使用 Markdown 格式進行筆記創建，並允許用戶將各個筆記通過雙向鏈接進行連接，
這使得它非常適合進行思維導圖、知識圖譜或者個人知識庫的管理。

## 瀏覽器

### Arc

[**Arc**](https://arc.net/) 是一款由 The Browser Company 開發的創新型瀏覽器，
旨在提供一個更加現代化且以生產力為導向的瀏覽器體驗。
Arc 打破了傳統瀏覽器的界限，設計上注重簡潔、直觀的用戶界面，並致力於提升使用者的工作流程效率。

### Zen Browser

[**Zen Browser**](https://zen-browser.app/) 的設計與 Arc 非常相似，
與 Arc 最大的不同是，Zen Browser 基於 Mozilla Firefox。

## 命令行工具

### bat

[**bat**](https://github.com/sharkdp/bat) 是一個 `cat` 替代品，用於在命令行中顯示文件內容。
它提供了語法辨識、行號顯示、分頁功能等，比傳統的 cat 更加直觀。

### fzf
[**fzf**](https://junegunn.github.io/fzf/) 是一個模糊搜尋工具，
可以在終端機中，以選單的方式搜尋檔案、指令紀錄、運行的程式...等。

也有非常多的工具可以與 fzf 結合，讓搜尋變得更加靈活。

### ripgrep

[**ripgrep**](https://github.com/BurntSushi/ripgrep) 是一款超快速的檔案內容搜尋工具， 用來取代傳統的 grep。
它比 grep、ack、ag（The Silver Searcher）更快，並且內建遞迴搜尋、忽略 `.gitignore` 規則。

### delta

[**delta**](https://github.com/dandavison/delta) 是一款美觀的 Git Diff Viewer，用來取代 git diff。
提供語法辨識、側邊欄、行內變更顯示，讓 git diff 變得更清晰易讀。
