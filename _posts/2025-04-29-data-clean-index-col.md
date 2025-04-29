---
title: 清理數據中的 Index 和 Column Name
date: 2025-04-29 18:17:25 +0800
categories: [Data, Data Basics]
tags: [data, pandas]     # TAG names should always be lowercase
math: false
---

清理數據的第一步就是對 index 和 column name 進行整理和修改，避免 index 和 column name 是非常混亂的。這部分包括，修改 index 和 column name 已經對 index 或 column 進行排序。

### 字典修改 index 和 column name

清理數據的第一步就是對 index 和 column name 進行整理和修改，避免 index 和 column name 是非常混亂的。想要修改 index 和 column name 成我們想要的值，可以用：

```python
df.rename(index = {"old_index_1": "new_index_1", "old_index_2": "new_index_2" })
```

想要修改 column name, 也是類似的，只需要把 `index` 這個關鍵詞改為 `columns`. 這個方法會返回修改過的 dataframe, 不會對原本的 dataframe 進行修改。如果想要直接修改原本的 dataframe, 可以使用`inplace`這個參數：

```python
df.rename(index = {"old_index_1": "new_index_1", "old_index_2": "new_index_2" }, inplace = True)
```



### 函數修改 index/column name

另外如果不想要一個個修改index和column name，我們可以傳入把函數傳入 index 和 column，例如我們想要把所有column name 改為大寫，那麼：
```python
df.rename(columns = str.upper, inplace = True)
```



### 對index/column name進行排序

想要對 index 或 column name 進行排序十分簡單，我們只需要：

```python
df.sort_index(axis = 0) # axis=0 就是在對index排序，axis=1 則是對 col name 排序
```

同樣地，這也會返回一個新的 Dataframe, 想要直接改變原有的 dataframe 的話，可以加上 `inplace`.
