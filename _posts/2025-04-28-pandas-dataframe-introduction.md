---
title: Pandas 簡介 —— Dataframe
date: 2025-04-28 18:46:41 +0800
categories: [Python, Python Basics]
tags: [pandas, data]     # TAG names should always be lowercase
math: false
---

接續上一篇介紹 `Series` 的文章，本文將介紹 `pandas` 中的 `Dataframe`。

## 創建 Dataframe

Dataframe 可以想象成是多個 Series 組成的字典。他的不同 column 可以是不同的數據類型，每個 column 都有自己的列名。下面來講如何創建一個 dataframe:

```python
import pandas as pd

# 建立三個 Series
s_id    = pd.Series(["01", "02", "03", "04", "05"])
s_class = pd.Series(["二班", "一班", "二班", "三班", "一班"])
s_grade = pd.Series([92, 67, 70, 88, 76])

# 建立 DataFrame
df1 = pd.DataFrame({
    "學號":  s_id,
    "班級":  s_class,
    "成績":  s_grade
})
```

結果：

```
   學號 班級  成績
0  01  二班  92
1  02  一班  67
2  03  二班  70
3  04  三班  88
4  05  一班  76
```

此外我們可以直接把 list 傳入，也就是說 `s_id`, `s_class` 以及 `s_grade` 可以直接是 list, 不需要加上 `pd.Series`. 我們也可以傳入有標籤索引的 `Series`，這樣 dataframe 的索引也會變成對應的索引。

## 常用屬性

* `dataframe.index` 可以獲取所有索引
* `dataframe.columns` 可以獲取所有 column 名字
* `dataframe.values` 可以獲得所有數據，返回的類型是 numpy array
* `dataframe.T` 可以獲得轉置後的 dataframe

## 提取 Dataframe 的 column

* `dataframe["column_name"]` 可以提取對應的 column，也可以通過 `dataframe.column_name`來提取對應的 column` `&#x20;
* 如果想提取多個 column 可以在方括弧內放入多個 column name 來獲取，`dataframe[["column_name1", "column_name2"]]`

## 提取 Dataframe 的 row

* 我們可以用 `loc` 和 `iloc` 提取 row，具體區別，請看 `Series` 的介紹文章
* `dataframe.loc[["row_name1", "row_name2"]]` 可以幫我們提取出多個 row
* `dataframe.loc["row_name","column_name"]` 可以幫我們提取出某個位置的數據，也可以結合切片來得到某個範圍的值，`dataframe.loc[row_slice, column_slice]`

## 條件篩選出符合條件的 row

* 和之前篩選 Series 類似，我們可以用 `dataframe[dataframa["column"] > 20]` 來篩選出符合條件的 row

## 添加/修改 Column

想要添加和修改 column 的方法是一樣的，我們可以先選定我們要修改或添加的 column 的名字，然後用以下幾種方法來添加：

* `df["column_name"] = pd.Series([data], index = [inedx])`, 注意這裡一定要加上對應的index
* `df["column_name"] = [data]`, 如果不想手動輸入對應的index的話，可以用這個方法，他會按照順序對齊
* 如果想修改的列名不存在就會添加對應的 column

## 添加/修改 row

* 添加 row 的方法和 上面類似，只是我們要用到 `loc`, 這裡要注意的是 `iloc` 是不能用來添加/修改 row 的

## 刪除 row/column

* 可以用 `df.drop(想要刪除的 row)` 來刪除，它會返回刪除後的 dataframa, 並不會對原本的 dataframe 修改
* `df.drop(想要刪除的 column, axis = 1)` 可以用來刪除 column

## Dataframe 的四則運算

Dataframe 在做四則運算的時候會對齊對應的 index 和 column 來做四則運算，如果其中一方沒有對應的話就會出現 NaN, 為了避免我們可以使用 `df1.add(df2, fill_value = 0)` 來操作。（add 可以替換成其他四則運算）

## Dataframe 與 Series 之間的運算

Dataframe 和 Series 之間也可以做運算，Series 的 index 會和 Dataframe 的 column 對齊，這可能有點難以理解，所以我們來看例子：

* Dataframe:

```
          Math  English  Science
Alice       80       85       88
Bob         90       95       92
Charlie     70       75       78
```

* Series:

```
Math       5
English    3
Science    2
dtype: int64
```

* Dataframe + Series:

```
          Math  English  Science
Alice       85       88       90
Bob         95       98       94
Charlie     75       78       80
```

可以看到每個 row 都會加上對應的值。

## 常用方法

* `df.head(n)` 可以返回前 `n` row 數據
* `df.describe()` 可以告訴我們各個 column 的統計信息
* `df.mean()` 告訴我們平均值，默認是 `axis = 0` 也就是告訴我們每個 column 的平均值，可選 `axis = 1`

## Apply 與 Applymap

如果我們想對每個 column 的數據做運算得到某個特殊的統計值，例如我們想要得到去掉最大和最小值的平均值，我們需要自己定義函數。使用 apply 方法，我們可以把每個 column 看做是輸入函數裡面的參數，然後得到對應的值。

例子：

```python
df = pd.DataFrame({
    "數學": [92, 85, 70, 88, 76],
    "英文": [67, 80, 90, 60, 75],
    "理科": [70, 65, 85, 90, 80]
})

# 定義一個函數：去掉最大值和最小值後，計算平均
def trimmed_mean(x):
    return (x.sum() - x.max() - x.min()) / (len(x) - 2)

# 使用 apply 對每個 column 套用這個函數
result = df.apply(trimmed_mean)

print("\n去掉最大最小值後的平均：")
print(result)
```

就能得到：

```
原始資料：
  數學  英文  理科
0  92  67  70
1  85  80  65
2  70  90  85
3  88  60  90
4  76  75  80

去掉最大最小值後的平均：
數學    83.0
英文    74.0
理科    78.333333
dtype: float64
```

如果想要對 row 做操作，可以使用參數 `axis = 1`.

如果想要操作每個元素而不是 row 或 column 的話，我們就要用 `df.applymap()`, 例子：`df.applymap(lambda x : x+5)`.
