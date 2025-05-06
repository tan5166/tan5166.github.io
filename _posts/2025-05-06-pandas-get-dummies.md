---
title: 用 `get_dummies` 將分類變數轉換為數值型資料
date: 2025-05-06 14:59:27 +0800
categories: [Data, Data Basics]
tags: [data, pandas]     # TAG names should always be lowercase
math: true
---

在使用線性回歸處理資料時，我們常會遇到**分類變數（categorical variables）**，例如性別（male/female）、地區（north/south/west）等。但線性回歾是一種只接受數值型資料的模型，這意味著我們必須先將這些文字型的類別資料轉換為數值格式，才能順利訓練模型。


這時，`pandas` 提供的 `get_dummies()` 函數就是非常實用的工具，它能夠將分類變數轉換成一組由 0 和 1 組成的欄位，這個過程就叫做 **One-Hot Encoding**。本文將簡單介紹如何使用 `get_dummies()`，並說明它在進行線性回歸前的重要性。

## 基本語法

使用的方法很簡單：

```python
pd.get_dummies(df, columns=["col_name"], dtype=int)
```

我們只需要把我們需要轉換的 column 以上面的形式傳入 `get_dummies` 中就可以。



需要注意的是，一般上來說，我們不會如果這個變數之間高度相關，又或者更進一步是線性相關的，就會導致我們無法求解出對應的線性回歸方程式，原因如下：

線性回歸中我們要求解的方程式為：

$$
\textbf{y} = \textbf{X}\beta + \epsilon
$$

而使用最小平方法可得：

$$
\beta = (\textbf{X}^T\textbf{X})^{-1} \textbf{X}^T \textbf{y}
$$

如果 $\textbf{X}$ 中有些變數為 linear dependent 就會導致 $\textbf{X}^T\textbf{X}$ 變為 singular matrix, 無法求得反矩陣。



所以，如果變數之間存在高度相關，我們便會在做線性回歸之前將其中之一捨棄。一般來說，pandas category 變數都是非此即彼，所以轉為 one hot encoding 之後，我們需要捨棄其中一個 column 來保證不會發生 linear dependent, 這時候我們可以加上 `drop_first = True`：

```python
pd.get_dummies(df, columns=["col_name"], dtype=int, drop_first=True)
```



> 使用 `df.corr()` 可以看到變數之間的 correlation.
