---
title: Numpy 簡介
date: 2025-04-27 16:14:02 +0800
categories: [Python, Python Basics]
tags: [numpy, data]     # TAG names should always be lowercase
math: false
---

在數據分析、機器學習以及各種科學計算的領域當中，高效處理數據都是重要的議題。而Numpy就是 python 中一個簡單好用且能提供較為高效的計算的一個庫。本文將介紹 Numpy，包括其基本語法、屬性、以及一些基本操作。

## 介紹

Numpy 提供的用於計算的資料結構是 array (數組)。Array 和 list 非常相似，唯一不同的是 numpy 的 array 只能儲存統一類型的元素，不能和 list 一樣擁有不同類型的元素。此外，Numpy 還提供了大量做數學運算的函數，比如求中位數、平均數、方差等等。

## 創建 Numpy 中的 array

使用 Numpy 的時候都需要先把它 import 進來，通常我們都會給他的別名是 `np`.

```python
import numpy as np
```

創建 array 的最簡單方法就是用 `np.array` 來把 list 轉換為 array:

```python
arr1 = np.array([1, 2, 3])
arr2 = np.array([[1, 2, 3], [4, 5, 6]]) #這是二維數組
```

### 更多創建 array 的方法

* `np.zeros(n)`: 創建一個長度為`n`，元素為0的 array，我們也可以直接傳入形狀，例如我們想要一個 2x3 的全零 array，我們就可以寫 `np.zeros((2, 3))`
* `np.ones(n)`: 創建一個長度為 `n`，元素為1的 array
* `np.arange(start, end, step)`: 創建一個 array，其中有 `[start, start + step, start + 2step, ...]`. 最後一個元素的會小於 `end`，因此用這個方法創建的array不會有 `end`.

## Array 的屬性

Array有一些屬性，例如：

* `ndim` 會告訴我們array的維度
* `shape` 會告訴我們array的形狀，例如 `arr2` 就是一個 2x3 的 array，所以會返回 `(2, 3)`
* `dtype` 會返回給我們array的類型，例如 `int64` 指的是64 bits的整數
* `itemsize` 會告訴我們一個元素佔用多少 byte.

## 常用操作

### Concatenate (拼接)

`concatenate` 是numpy中常用的方法可以把多個array拼接在一起，例子：

```python
arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])
arr3 = np.array([7, 8, 9])
np.concatenate((arr1, arr2, arr3), axis=0)
```

這裡的 `axis = 0` 的意思是，我們可以想象成我們堆疊的方法是新增更多的 `row`. 由於 `arr1,2,3` 的形狀都是 `(3,)` 所以得到的最後 array 是一個形狀為 `(9, )` 並且元素為 `[1, 2, 3, ..., 9]`的array. 值得注意的是，這裡並不能沿著 `axis=1` 合併，如果要沿著 `axis = 1` 合併，我們需要用到 `reshape`.

### Reshape

`reshape` 是用來改變 array 形狀的方法，例如我們可以通過它把 `arr1` 變成 1x3 的形狀。

```python
arr1 = arr1.reshape(1, 3)
```

如果我們要沿著 `axis = 1` 把他們合併成如下形狀：

```lua
[[1 2 3]
 [4 5 6]
 [7 8 9]]
```

那我們需要把三個array都變成 3x1 的形狀：

```python
arr1 = arr1.reshape(3, 1)
arr2 = arr2.reshape(3, 1)
arr3 = arr3.reshape(3, 1)

result = np.concatenate((arr1, arr2, arr3), axis=1)
```

### Sort

Numpy 中有提供兩種排序array的方法，他們只有細微區別：

* `np.sort(arr)`: 這個方法會在排序好之後，把排序 array 返回，不會改變原本的 array
* `arr.sort()`: 這會sort原本的array, 原本的array 會發生變化

### Index

除了一般用正整數的index 來獲得特定位置的元素之外，我們還可以用負數來得到特定位置的元素，例如：`arr[-1]` 為最後一個元素，`arr[-2]`為最後第二個元素，以此類推。

此外，我們還可以用 slice 的方法來獲得 subarray, 例如： `arr[1:4]`可以獲得 index 為 1 到 index 為 3 的元素，結束索引並不會被包含進去。

再來，我們還可以通過條件篩選得到符合條件的元素，例如：`arr[(arr > 2) & (arr < 10)]` 就能得到大於2小於10的所有元素。
