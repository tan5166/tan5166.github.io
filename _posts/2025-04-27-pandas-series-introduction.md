---
title: Pandas 簡介 —— Series
date: 2025-04-27 21:22:20 +0800
categories: [Python, Basics]
tags: [pandas]     # TAG names should always be lowercase
math: false
---

Pandas 是一個基於 Python 的資料處理與分析工具，它提供了高效且靈活的資料結構，使處理結構化資料（如表格、時間序列等）變得更加簡單。Pandas 建立在 NumPy 之上，充分利用了 NumPy 的高效數值運算能力，同時引入了更高層次的資料操作介面，例如 `DataFrame` 和 `Series`，讓資料的讀取、篩選、清理、轉換與統計分析更加直觀和強大。本文將介紹 `pandas` 中的 Series。

## Series

`Series` 是一種帶有索引的一維資料結構，類似於一個可以標上名字的陣列。每個資料值旁邊都有一個對應的索引（index），可以用索引快速地取出或操作資料。即使資料的順序改變，只要有索引在，也能輕鬆定位到正確的值。創建一個 `Series` 非常簡單：

```python
import pandas as pd

data = pd.Series([10, 20, 30, 40, 50])
print(data)
```

我們就能得到

```lua
0    10
1    20
2    30
3    40
4    50
dtype: int64
```

左邊的是索引，右邊的是值。我們可以在 `Series` 中自己定義索引,

```python
import pandas as pd

data = pd.Series([10, 20, 30], index=['a', 'c', 'b', 'f', 'k'])
print(data)
```

就能得到，

```lua
a    10
c    20
b    30
f    40
k    50
dtype: int64
```

這樣做的好處是，我們可以通過我們定義的索引來獲取特定元素，例如：`data["a"]`, 當然原先的索引方法仍然是可以用的。為了區別開來，我們把原先的索引叫做 “**位置索引**”，我們自己定義的叫做 “**標籤索引**”。這兩個索引有細微不同之處：

* 位置索引：`data[1:3]` 不包含結尾索引
* 標籤索引：`data[“a”:"c"]` 包含結尾索引，所以會輸出前兩項

我們還可以放入一個列表來進行索引，例如：

```python
data[["f", "a", "k"]] # 結果和 data[["3", "0", "4"]]
```

就能得到

```lua
f    40
a    10
k    50
dtype: int64
```

## loc 和 iloc

當然爾，我們還可以用整數作為標籤，但這可能讓我們發生困惑，不知道索引取值和切片取值的時候是用哪一個。其實結果是：

* 索引取值按照**標籤**
* 切片取值按照**位置**

為了避免這種困惑，Pandas 提供給我們 `loc` 和 `iloc` 方法，`loc` 表示用標籤索引，`iloc` 表示用位置索引。使用方法如 `data.iloc[3]`

## 條件篩選

和 Numpy 裡的 array 一樣，我們也可以通過條件篩選符合條件的元素，例如: `data[(data > 20) | (data < 40)]`

## 字典創建 Series

我們還可以直接傳入一個字典用來創建 Series：

```python
data = pd.Series({
    "青菜": 4.1,
    "白蘿蔔": 2.2,
    "西紅柿": 5.3,
    "土豆": 3.7,
    "黃瓜": 6.8
})
```

這樣key就對變成對應的index.

## 四則運算

在 Series 當中，我們也可以使用加減乘除來操作，只有擁有同樣索引的值會被加起來，其餘的都會變成 NaN. 例如：

```python
s1 = pd.Series([1, 2, 3, 4, 5], index = ['a', 'b', 'c', 'd', 'e'])
s2 = pd.Series([50, 40, 30, 20, 10], index = ['a', 'b', 'd', 'e', 'f'])
```

`s1+s2` 就會得到：

```lua
a    51.0
b    42.0
c     NaN
d    34.0
e    25.0
f     NaN
dtype: float64
```

如果希望缺失的值有默認的話，可以使用 `s1.add(s2, fill_value=0)`.  這樣的話可以得到：

```lua
a    51.0
b    42.0
c     3.0
d    34.0
e    25.0
f    10.0
dtype: float64
```

## 常用方法

* `min, max, mean, sum` 這些常用的方法也出現在 Series當中
* `describe` 方法可以告訴我們一些重要的統計信息

## 對元素分別操作

如果想要對每個元素分別操作，例如，我們擁有 `scores` 這個記錄了全班分數的 Series，我們想要設置 80 分以上為 A，60分以上為 B，其餘為 C 的話，我們可以先定義：

```python
def grade_from_score(score):
  if score >= 80:
    return "A"
  elif score >= 60:
    return "B"
  else:
    return "C"
```

然後使用 `apply`，他會返回一個新的Series：

```python
grades = scores.apply(grade_from_score)
```

我們也可以傳入匿名函數，關於匿名函數，詳見本 blog 中相應文章。
