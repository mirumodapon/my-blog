---
date: '2025-01-05T23:29:49+08:00'
draft: true
title: '螞蟻演算法 - Python 範例'
image: cover.webp
tags:
  - algorithm
---

前陣子，我的女朋友帶著一臉焦急來找我求救，說她需要完成一個關於**螞蟻演算法**的報告，但完全不知道怎麼做，希望我幫幫他。「作業要自己做！」看了一下我的行程然後跟她說了這句話。

。  
。  
。  

「好啦！」   
（專案 PR 我還沒 Review 完耶 QAQ ~）  

。  
。  
。

❗️❗️ 女朋友表示：以上純屬虛構 ❗️❗️ 

## 什麼是螞蟻演算法？
螞蟻演算法（Ant Colony Optimization, ACO）是一種受自然界啟發的優化演算法，
其靈感來源於螞蟻群體尋找食物時的集體行為。
這個演算法由義大利科學家 Marco Dorigo 在 1992 年提出，
並在後續的研究中被廣泛應用於解決各種複雜的組合優化問題。

螞蟻在探索食物時，會在經過的路徑上釋放費洛蒙，
費洛蒙的濃度越高，其他螞蟻選擇這條路徑的機率也越大。
然而，費洛蒙會隨時間揮發，因此如果一條路徑較長或效率較低，
費洛蒙的吸引力會逐漸減弱。
相反的，短而有效的路徑會因為更多螞蟻的選擇而累積更多費洛蒙，最終成為群體的最優選擇。螞蟻演算法的核心在於模擬這一過程，通過不斷迭代來逼近最優解。

## 螞蟻演算法的步驟

螞蟻演算法通過以下幾個步驟來模擬螞蟻的行為：

1. 初始化：設定蟻群的活動空間，這個空間通常用來代表問題的解決範圍或解空間。同時，也會設定費洛蒙的初始濃度和其他參數。

2. 解的構建：蟻群中的螞蟻開始在活動空間中隨機遊走，根據費洛蒙濃度和啟發式資訊選擇路徑。

3. 費洛蒙更新：每當一隻螞蟻完成了一次解的建構，演算法便會更新這段路徑上的費洛蒙值。有效的路徑會獲得更多的費洛蒙，反之則會減少。

4. 迭代：重複步驟2和3，直到達到停止條件，如固定的迭代次數或解的改進程度不再顯著。

通過這些步驟，螞蟻演算法能夠在解空間中發現隱藏的最佳解，並適應各種複雜的問題。

```pseudocode
procedure ACO_MetaHeuristic is
    while not terminated do
        generateSolutions()
        daemonActions()
        pheromoneUpdate()
    repeat
end procedure
```

## 螞蟻的路徑選擇

螞蟻在選擇路徑時，主要依賴於費洛蒙的濃度。
具體來說，當濃度越高時，螞蟻選擇該路徑的機率也越高，
我們用以下公式來表示螞蟻從當前節點 \(i\) 選擇下一個節點 \(j\) 的機率：

$$
P_{ij} = \frac{\tau_{ij}^{\alpha} \eta_{ij}^{\beta}}{\sum_{k \in N_i} \tau_{ik}^{\alpha} \eta_{ik}^{\beta}}
$$

其中：
- \(\tau_{ij}\) 代表從節點 \(i\) 到節點 \(j\) 的費洛蒙濃度。
- \(\eta_{ij}\) 代表啟發式資訊（該問題的結果優劣），通常是距離的倒數 \(\frac{1}{d_{ij}}\)。
- \(\alpha\) 和 \(\beta\) 是兩個參數，分別控制費洛蒙與啟發式資訊的影響程度。
- \(N_i\) 為當前螞蟻可選擇的鄰近節點集合。

當 \(\alpha\) 值較大時，螞蟻更傾向於選擇費洛蒙濃度高的路徑，
而當 \(\beta\) 值較大時，則更強調啟發式資訊（如較短的距離）。
適當調整這些參數，能夠提升演算法的性能。

## 費洛蒙的更新

費洛蒙更新機制確保了有效路徑的增強與次優路徑的淘汰。更新過程通常包含兩個部分：

1. 費洛蒙蒸發：為了避免過早收斂至局部最優解，費洛蒙會隨時間逐漸減少，其衰減公式為：

    $$
    \tau_{ij} \leftarrow (1 - \rho) \cdot \tau_{ij}
    $$

    其中，\(\rho\) 為蒸發率（0 < \(\rho\) < 1），用來控制費洛蒙的衰減速度。

2. 費洛蒙增強：當螞蟻成功找到解後，根據路徑長度分配新的費洛蒙：

    $$
    \tau_{ij} \leftarrow \tau_{ij} + \sum_{k=1}^{m} \Delta \tau_{ij}^{k}
    $$

    其中，\(\Delta \tau_{ij}^{k}\) 為第 \(k\) 隻螞蟻在路徑上的費洛蒙貢獻，
    通常與解的品質相關，例如：\(\Delta \tau_{ij}^{k} = \frac{Q}{L_k}\)。

    - \(Q\) 為常數，用來調整費洛蒙的強度。
    - \(L_k\) 為第  隻螞蟻找到的解的路徑長度，越短的路徑獲得的費洛蒙越多。

## 實作範例

最後，為了展示螞蟻演算法的應用，這裡以旅行推銷員問題（[TSP](https://en.wikipedia.org/wiki/Travelling_salesman_problem)）為例。
TSP 的目標是尋找最短路徑，使旅行推銷員能夠走訪所有城市且最終返回起點。


[![](https://opengraph.githubassets.com/29fd19c671af65614e5fae3b201cdc010df3618ae56b978e523185004c914d7c/mirumodapon/ant-colony-optimization-python-example)](https://github.com/mirumodapon/ant-colony-optimization-python-example)

---
<h4>參考資料</h4>

- [wikipedia - Ant colony optimization algorithms](https://en.wikipedia.org/wiki/Ant_colony_optimization_algorithms)

<h4>圖片來源</h4>

- 封面圖片：GPT 生成
