---
title: 拼接與合併 Dataframe
date: 2025-05-01 18:06:20 +0800
categories: [Data, Data Basics]
tags: [data, pandas]     # TAG names should always be lowercase
math: false
---

在實際的資料分析過程中，我們常常會遇到來自不同來源的資料。例如，一份是顧客資料表，一份是訂單紀錄表；或者是不同月份的交易記錄。這時候，我們就需要把這些資料整合在一起，方便進一步分析。整合的方式主要有兩種：

- 縱向拼接（垂直疊加資料）
- 橫向拼接（左右並排欄位）
- 合併（類似 SQL 的 join 操作）



## 拼接 Dataframe

### 縱向拼接 Dataframe

如果你有兩份結構相同（也就是欄位名稱一樣）的資料，例如兩個月份的交易記錄，可以用 `pd.concat()` 直接把它們上下接起來：

```python
pd.concat([df1, df2])
```

預設情況下，`concat` 會保留原本的 index。如果你不需要保留舊的 index，可以加上：

```python
pd.concat([df1, df2], ignore_index = False)
```

這樣就會返回新的從零開始的位置索引。



### 橫向拼接 Dataframe

當你想要把兩份資料「左右並排」放在一起時，可以這麼做：

```python
pd.concat([df1, df2], axis = 1)
```

這個方法會根據 index 來對齊資料，因此需要確保 `df1` 和 `df2` 的 index 是對得上的。

若兩個 Dataframe 的 row 數量不一致，會自動補上 `NaN`，表示該位置無對應資料。



## 合併 Dataframe

### Merge

如果你習慣使用 SQL 的 join 語法，`pandas.merge()` 就是類似的工具。舉個例子，如果你有「訂單資料 df_orders」和「顧客資料 df_customers」，兩邊都用 `CustomerID` 做鍵值，那你可以這麼做：

```python
df_result = pd.merge(df_orders, df_customers, on="CustomerID", how="inner")
```

| 參數                   | 功能                                                                                        |
| ---------------------- | ------------------------------------------------------------------------------------------- |
| `on`                   | 指定兩邊共同的欄位名稱作為鍵                                                                |
| `left_on` / `right_on` | 如果兩邊鍵的欄位名稱不一樣，可以分別指定                                                    |
| `how`                  | 合併方式：`"inner"`（交集），`"outer"`（聯集），`"left"`（左表為主），`"right"`（右表為主） |



### Join

如果你想根據 index 而不是欄位值來合併資料，可以用 `df.join()`：

```python
df_result = df1.join(df2, how="left", lsuffix="_left", rsuffix="_right")

```

- 預設是按 index 合併

- 如果兩邊有相同欄位名稱，需要用 `lsuffix` 和 `rsuffix` 指定區分用的字尾
