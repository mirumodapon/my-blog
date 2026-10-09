---
date: '2026-10-08T21:30:11+08:00'
title: Rush Worktree 共用依賴與快取
image: cover.webp
tags:
  - rushjs
  - monorepo
  - worktree
---

最近到了新的公司，關於心情的部分，有機會再寫個心得文（看我這發文頻率，應該知道要幾百年後了），總結一下入職一個禮拜的一句話「有種被當人的感覺了」。

在公司的的專案用的是 rushjs 的 monorepo，rushjs 是微軟開發的 monorepo 工具，在這個這麼大的 monorepo  裡面，用到 worktree 的機會又更多了。

## rush 的資料不是共用的？

Rush.js 是一套用來管理 JavaScript / TypeScript Monorepo 的工具鏈，由 Microsoft 維護，屬於 Rush Stack 生態系。其中一個特點就是，Rush 會使用 link 來建立 node_modules，這個操作類似於 pnpm 的依賴安裝方式，如果熟悉 pnpm  的朋友就知道，pnpm  的依賴其實是放在家目錄（~/.pnpm-store），因此在多個專案當中，同個依賴會安裝在家目錄當中，各個專案當中的 `node_modules` 會用 link 的方式連過去。

而在 rush 當中，也做了這件事情，只不過他預設是安裝在 `<project>/common/temp/<...>` 當中，也就是說，如果我有多個 rushjs 的專案，這些依賴是不會共用的，想當然的如果我開了多個 worktree，rush 會在每個 worktree 當中都安裝一份依賴。

除了依賴以外，rush 在建置這些 package 的時候，會保存建置的快取，而這些快取會在下次建置時被使用，這些快取資料預設也是存在 `<project>/common/temp/build-cache` 當中，也是在 worktree 之間不會被共用。

## 修改 rush 依賴的儲存路徑

如果使用 `pnpm` 我們可以很輕易的透過設定環境變數([ref](https://rushjs.io/pages/configs/environment_vars/#rush_pnpm_store_path))來改變儲存路徑

```Bash
$ RUSH_PNPM_STORE_PATH=~/.rush/.pnpm-store rush install
```

也可以加到 `.bashrc` 或是 `.zshrc` 裡：

```Bash
export RUSH_HOME=~/.rush
export RUSH_PNPM_STORE_PATH="$RUSH_HOME/.pnpm-store"
```

## 修改 build cache 的儲存路徑

在文件當中，有這麼一段話([ref](https://rushjs.io/pages/maintainer/build_cache/#docusaurus_skipToContent_fallback))

> **In a cache folder on your local disk.** This way you can switch between different branches without losing your incremental build state. ==You can even configure a centralized folder to be shared between multiple enlistments on your machine.== The default location is **common/temp/build-cache**.

但翻了一整個早上的文件，我還是找不到哪裡可以修改這個路徑。索性直接暴力翻源碼。

<details>
    <summary>Code Stack</summary>
    
https://github.com/microsoft/rushstack/blob/e2341a3fcacd6a25263e4c35ccd7c9fdda676e3b/libraries/rush-lib/src/schemas/rush-user-settings.schema.json#L13
    
https://github.com/microsoft/rushstack/blob/e2341a3fcacd6a25263e4c35ccd7c9fdda676e3b/libraries/rush-lib/src/api/RushUserConfiguration.ts#L52

https://github.com/microsoft/rushstack/blob/e2341a3fcacd6a25263e4c35ccd7c9fdda676e3b/libraries/rush-lib/src/api/RushUserConfiguration.ts#L35

https://github.com/microsoft/rushstack/blob/e2341a3fcacd6a25263e4c35ccd7c9fdda676e3b/libraries/rush-lib/src/logic/RushConstants.ts#L9
</details>

最後我們可以在家目錄當中建立 `.rush-user` 並且在裡面加入 `settings.json`:

```JSON
{
    "buildCacheFolder": "~/.rush/build-cache"
}
```

這樣設定完之後，所有的 worktree 就可以共用快取啦！！


---
<h4>參考資料</h4>

- [rushstack github](https://github.com/microsoft/rushstack)
- [rush docs](https://rushjs.io)
