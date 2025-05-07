---
title: Static Collection 和 Live Collection 的差異
date: 2025-05-07 13:52:33 +0800
categories: [Web Development, JavaScript]
tags: [dom, javascript, html, css]     # TAG names should always be lowercase
math: false
---

在操作 DOM 時，我們經常會使用 JavaScript 取得一組 HTML 元素進行操作，例如：

```javascript
document.getElementsByClassName("item");
document.querySelectorAll(".item");
```

這些方法表面上功能類似，實際上它們回傳的是不同型態的集合（collection），而這些集合的是否會自動反映 DOM 變化，決定了我們應該如何使用它們。



## 什麼是 Live Collection？

Live Collection 指的是，當 DOM 結構改變時（例如新增或刪除元素），集合內容會自動更新。

### 常見的 Live Collection 方法：

- `getElementsByClassName()`
- `getElementsByTagName()`
- `element.children`

### 回傳類型：

- `HTMLCollection`（不支援 `forEach()`，需要轉為陣列）

### 特性：

- 與 DOM 維持同步（Live）
- 節省重新查詢的成本



##  什麼是 Static Collection？

Static Collection 指的是，取得集合時是 DOM 當下的快照，之後 DOM 再變動也不會影響集合內容。

### 常見的 Static Collection 方法：

- `querySelectorAll()`
- `element.childNodes`

### 回傳類型：

- `NodeList`（支援 `forEach()`）

### 特性：

- 一次性查詢結果（不會自動更新）
- 較穩定、預測性高，適合搭配迴圈與邏輯處理



## 差異示意範例

```javascript
const liveList = document.getElementsByTagName("li");     // Live
const staticList = document.querySelectorAll("li");       // Static

console.log(liveList.length);   // 2
console.log(staticList.length); // 2

// 新增一個 <li>
const newLi = document.createElement("li");
document.querySelector("ul").appendChild(newLi);

console.log(liveList.length);   // ✅ 自動變為 3
console.log(staticList.length); // ❌ 仍然是 2
```



##  何時該用 Live Collection？

| 適合情境                                               | 原因                                  |
| ------------------------------------------------------ | ------------------------------------- |
| 畫面上元素會**不斷新增或刪除**，例如留言清單、待辦清單 | 集合會自動反映 DOM 更新，避免重複查詢 |
| 需要監控某一組元素是否變動                             | 無需額外監控機制即可同步獲得最新狀態  |



## 何時該用 Static Collection？

| 適合情境                                                      | 原因                                 |
| ------------------------------------------------------------- | ------------------------------------ |
| 只需要**當下的一組元素**進行處理                              | 靜態集合邏輯清晰、效能更高           |
| 搭配 `forEach()` 進行遍歷                                     | `NodeList`（Static）原生支援迭代操作 |
| 需要避免因 DOM 更新導致集合變化的副作用（例如刪除元素時跳過） | Static 集合不變動，行為可預測        |
