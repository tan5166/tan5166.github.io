---
title: Pandas 簡介 —— 關於 CSV
date: 2025-04-28 21:56:26 +0800
categories: [Python, Python Basics]
tags: [pandas, csv, data]     # TAG names should always be lowercase
math: false
---

## 讀取

要在 pandas 中讀取 csv 非常簡單，我們只需要：

```python
df = pd.read_csv("path")
```

一行就能讀取。他會把原文件的第一個 row 作為 column name. 但如果原本的文件沒有column name，我們可以：

```python
df = pd.read_csv("path", header = None)
```

值得一提的是第一個 column 並不會被解析成 index, 如果你希望某個 column 被解析成 index 可以：

```python
df = pd.read_csv("path", index_col = "column_name")
```

## 顯示

如果文件中有很多 column, 那中間的 column 在顯示的時候可能會被忽略。如果我們還是想看所有的 column，我們可以用：

```python
pd.set_option("display.max_columns", num)
```

其中 num 是一個數字，你可以用它來決定最多要顯示多少 column.

還有時候，某些值太長顯示不出來，我們想要讓他顯示出來，我們可以：

```python
pd.set_option("display.max_colwidth", num)
```
