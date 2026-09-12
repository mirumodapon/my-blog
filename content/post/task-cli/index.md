---
date: '2026-09-10T17:24:50+08:00'
title: 我真的需要這個 Todo CLI 嗎？
image: cover.webp
tags:
  - cli
---

感覺好像應該要逼自己多寫一點部落格（？

最近找了一些關於 task manager 或是 todo 的 cli 工具，感覺用起來都不太上手，問了一些人，大家都認為沒有這個 cli 工具的必要。

但！！

不覺得這東西有 TUI 很酷嗎 (ﾉ◕ヮ◕)ﾉ*:･ﾟ✧


## 想要的功能

大概想了一下，應該會把這東西設計成可以用 cli 的方式操作，同時也有 tui 介面可以用。那語言的部分就挑最近常寫的語言 Go 作為開發的語言，但是...我只是 Go 的初學者，目前只寫了一個小網站後端，我超廢！！所以我找了一下 Claude 大大來幫我，首先啟用 [superpower](https://github.com/obra/superpowers) 這個 skills，來防止他幻想，剩下的都讓他來問我囉！


>使用 Go 語言，做一個 todolist(task manager)，這個工具同時具有 cli 與 tui 的功能。


接下來， Claude 大大就會針對這個需求問我一堆問題，來確保這個專案的目標：


> **1. 這個 CLI + TUI 工具主要要做什麼？**
> - [x] 本機待辦事項管理
> - [ ] 搭配後端服務的 todo client
> - [ ] 待辦 + 其他功能（筆記/時間追蹤等）
>
> **2. CLI 和 TUI 兩邊的分工你想成怎樣？**
> - [ ] CLI 為主，TUI 是瀏覽模式
> - [ ] TUI 為主，CLI 只做快捷新增
> - [x] 兩者功能完全對等
>
> **3. 一條待辦除了「標題 + 完成與否」，還需要哪些欄位？（可複選，沒選的就不做）**
> - [x] 專案 / 分類（project）
> - [x] 標籤（tags）
> - [x] 截止日（due date）
> - [x] 優先度（priority）
>
> **4. 新增待辦時，這些欄位怎麼打？**
> - [ ] 內嵌語法（一行搞定）
> - [x] flag 為主
> - [ ] 內嵌語法 + flag 都支援
>
> **5. TUI 瀏覽模式裡，除了上下移動看清單，還能做什麼？（可複選）**
> - [x] 勾完成 / 取消完成
> - [x] 刪除
> - [x] 過濾 / 搜尋
> - [x] 編輯欄位
>
> **6. 技術方案選哪個？**
> - [ ] A：Cobra + Bubble Tea + JSON（推薦）
> - [x] B：Cobra + Bubble Tea + SQLite
> - [ ] C：標準庫 flag + tview
>
> **7. 除了 `-p` 自動拿 pwd，還需要手動指定專案名嗎？**
> - [ ] 只要 pwd 模式
> - [ ] `-p` 拿 pwd，`--project` 給名稱
> - [x] 同一個 flag，值可選
>
> **8.「當天顯示時間」需要截止日帶時刻，你想要哪一種？**
> - [x] 截止日可選帶時刻
> - [ ] 顯示建立時間
> - [ ] 先不做

接著就燃燒 Token 的時間啦！

啊？你說沒有技術成分？！<del><small>與其去買那些 AI 課程，不如 Donate 給我</small></del>   
沒啊！我只是想要炫耀我做的酷酷 TUI 而已

[![](https://opengraph.githubassets.com/21c1fcfd38fa62952ca8f10be6b99ef23ac06a8fab10b4c1d02d95c1a537d790/mirumodapon/task-cli)](https://github.com/mirumodapon/task-cli)
