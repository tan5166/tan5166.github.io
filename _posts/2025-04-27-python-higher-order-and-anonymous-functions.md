---
title: Python 高階和匿名函數
date: 2025-04-27 00:18:42 +0800
categories: [Python, Basics]
tags: []     # TAG names should always be lowercase
math: false
---

## 高階函數

在 Python 中可以可以把函數作為參數傳入函數當中，這種接收函數作為參數的函數被稱為**高階函數**，這提供給了我們更多靈活度。例子：

```python
def calculate_and_print(num, calculator):
  result = calculator(num)
  print(f"num: {num}, result: {result}")
```

## 匿名函數

有些時候我們定義一個函數可能只使用了一次，如果給這個函數想個名字略顯浪費，因為我們就只用那一次。這時候**匿名函數**就能派上用場：

```python
calculate_and_print(7, lambda num : num * num)
```

如果這個函數是多參數的，那我們可以在冒號前加上其它參數，例如：`lambda num1, num2: num1 + num2`。我們也可以直接調用匿名參數：

```python
(lambda num1, num2: num1 + num2)(2, 3)
```

Remark: 匿名函數不能寫太複雜的函數。
