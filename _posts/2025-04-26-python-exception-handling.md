---
title: Python 異常處理
date: 2025-04-26 17:06:32 +0800
categories: [Python, Basics]
tags: []     # TAG names should always be lowercase
math: false
---

寫程式的時候不免會遇到bug引起的異常錯誤，這篇文章旨在說明python中常見的異常類型，以及我們可以如何去捕捉這些異常。

## 常見異常類型

* 超出索引範圍 Index Error
* 不小心除以零 ZeroDivisionError
* 打開文件不存在 FileNotFoundError
* 類型不對引起的錯誤 TypeError
* 等等

## 捕捉異常

更多時候可能是用戶使用程序不規範導致的錯誤。例如：我們指示用戶輸入數字的時候，用戶卻輸入了文字，導致異常，程式停擺。當這種發生異常的時候，用戶可能並沒有發覺到他做錯了什麼，只覺得程序莫名停擺了，因此，我們需要對可能發生的錯誤進行輸出，告訴用戶發生的錯誤。Python中可以使用 `try` 和 `except` 來處理這類問題：

```python
try:
  user_weight = float(input("請輸入體重(kg)："))  
  user_height = float(input("請輸入身高(cm)"))
  user_BMI = user_weight/user_height ** 2
except ValueError:
  print("輸入不為數字，重新運行程式，並輸入合理的數字")
except ZeroDivisionError:
  print("身高不能為零，請重新運行程式，輸入正確數字")
except: #任何其他異常都會觸發
  print("發生了未知錯誤，請重新運行")
else: #如果沒有任何異常，則會觸發這條
  print(f"BMI: {user_BMI}")
finally: #無論有無異常，都會執行
  print("程序結束執行")
```
