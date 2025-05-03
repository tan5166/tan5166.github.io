---
title: 用query進行條件篩選
date: 2025-05-03 18:24:47 +0800
categories: [Data, Data Basics]
tags: [data, pandas]     # TAG names should always be lowercase
math: false
---

在進行資料分析時，我們經常需要根據特定條件來篩選資料。除了使用傳統的布林索引（Boolean Indexing）方式外，Pandas 也提供了一個更簡潔、類似 SQL 的語法：`query()`。

本文將透過簡單易懂的範例，教你如何使用 `query()` 來快速篩選出符合條件的資料。

我們以下列數據為例子：

```python
import pandas as pd

data = {
    '班級': ['A', 'A', 'B', 'B', 'C', 'C'],
    '姓名': ['小明', '小美', '小華', '小強', '小安', '小傑'],
    '性別': ['男', '女', '男', '男', '女', '男'],
    '成績': [85, 90, 78, 82, 95, 70]
}

df = pd.DataFrame(data)
print(df)
```



若我們想找出成績大於 80 分的學生，可以使用：

```python
df.query('成績 > 80')
```

就能得到大於 80 分的學生：

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>班級</th>
      <th>姓名</th>
      <th>性別</th>
      <th>成績</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>小明</td>
      <td>男</td>
      <td>85</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A</td>
      <td>小美</td>
      <td>女</td>
      <td>90</td>
    </tr>
    <tr>
      <th>3</th>
      <td>B</td>
      <td>小強</td>
      <td>男</td>
      <td>82</td>
    </tr>
    <tr>
      <th>4</th>
      <td>C</td>
      <td>小安</td>
      <td>女</td>
      <td>95</td>
    </tr>
  </tbody>
</table>


再來，如果想要多條件查詢，我們可以用 and 和 or，例如下面的語句就能查詢成績大於80的男性：

```python
df.query('成績 > 80 and 性別 == "男"')
```

結果如下：

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>班級</th>
      <th>姓名</th>
      <th>性別</th>
      <th>成績</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A</td>
      <td>小明</td>
      <td>男</td>
      <td>85</td>
    </tr>
    <tr>
      <th>3</th>
      <td>B</td>
      <td>小強</td>
      <td>男</td>
      <td>82</td>
    </tr>
  </tbody>
</table>
