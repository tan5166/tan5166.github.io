---
title: Element Node 與 Text Node, Comment Node 的差異
date: 2025-05-07 15:35:00 +0800
categories: [Web Development, JavaScript]
tags: [dom, javascript, html, css]     # TAG names should always be lowercase
math: false
---

在操作 DOM（Document Object Model）時，我們經常會接觸到三種常見的節點類型：

1. **Element Node**：對應 HTML 中的標籤（如 `<div>`、`<p>` 等）。
2. **Text Node**：表示元素中的文字內容。
3. **Comment Node**：表示 HTML 中的註解（如 `<!-- 註解內容 -->`）。

這三種節點在行為與屬性上有一些重要差異，以下整理說明。

## 使用 childNodes 和 children

* `childNodes`：會返回所有類型的子節點，包括元素節點、文字節點與註解節點，回傳類型為 `NodeList`。
* `children`：僅返回元素節點（`Element Node`），回傳類型為 `HTMLCollection`。

只有 **Element Node** 具備 `children` 屬性；Text Node 與 Comment Node 沒有這個屬性，只能使用 `childNodes`（通常也會是空的，因為它們無子節點）。
