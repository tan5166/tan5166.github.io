---
title: 讓數據變得乾淨 —— 整理數據集的內容
date: 2025-04-30 17:28:20 +0800
categories: [Data, Data Basics]
tags: [data, pandas]     # TAG names should always be lowercase
math: false
---

在做數據分析時，如果數據內容是有問題的話，必然會影響到我們的分析，而什麼是有問題的數據可以參考這一篇：[評估數據的整潔與乾淨度](https://tan5166.github.io/posts/data-tidy-clean-eval/). 本文章旨在說明如何使用 pandas 中的工具去對這些有問題的內容做修改，讓數據變得乾淨。



## 處理數據空缺

### 添加空缺值

數據分析中經常會遇到數據缺失的問題，有時候會需要我們手動添加上缺失的值，以下是幾種方法：

#### 自己定位並修改缺失值

如果遇到一整個 column 的缺失值，我們可以 `df["col_name"] = value` 來直接填補上他。此外，我們也可以用 `.loc` 來填補上一個區塊的空缺值，例如：`df.iloc["index", "col_name"] = value`.



#### `fillna` 定位空缺值

除了自己定位空缺值之外，我們還可以使用`fillna` 來填補空缺值，例如：對於某 column 的空缺值我們可以一律填上 0，`df["col_name"].fillna(0)`.

如果有多個 columns 要處理，並且每個要填上不同的值，我們可以把字典傳入 `fillna`. 例如：

```python
df.fillna({"col_name1": value1, "col_name2": value2})
```



### 刪除有空缺值的 row

除了自己添加上內容外，我們還可以用刪掉有空缺值的位置來解決數據裡有空缺值的問題。`dropna` 可以被用來幫我們處理這件事情。

- `df.dropna()` 可以刪除掉有空缺值的 row, 只要這個 row 的其中一個位置是 NaN.

- 如果希望只有當某些位置是空的時候才刪除，我們可以使用 `subset` 這個參數：

  ```python
  df.dropna(subset=["col_name1", "col_name2"])
  ```



## 處理數據重複

我們可以用 `drop_duplicates` 來把重複的 row 刪除，預設會保留第一次出現的 row，其餘重複的會被刪掉。

```python
df.drop_duplicates(subset=None, keep='first')
```

- `subset`：指定根據哪些 column 來判斷是否重複。如果不寫，預設是整個 row 完全相同才算重複。
- `keep='first'`：保留第一個出現的（預設），也可以用 `'last'` 或 `False`（全部刪掉）。



## 處理數據不一致

遇到數據不一致的時候，我們可以把數據替換成一致的格式。這時候 `replace` 就能排上用場。例如，有些欄位中「男」被寫成 `"男"`, `"male"`, `"M"`，為了後續分析方便，我們可以把這些不同寫法統一為 `"男"`。

```python
df["性別"].replace(["M", "male", "boy"], "男")

```

我們也可以用字典來實現多對多的替換：

```python
df["性別"].replace({"M": "男", "F": "女"})
```



> 不要忘記，以上這些操作並不會直接修改原本的 dataframe, 還需要加上 `inplace = True`.

