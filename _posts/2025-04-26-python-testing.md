---
title: Python 測試
date: 2025-04-26 17:53:41 +0800
categories: [Python, Python Basics]
tags: []     # TAG names should always be lowercase
math: false
---

由於我們不可能避免程序在發佈後發生錯誤，因此我們需要在程式發佈給用戶之前做好測試，減少可能發生的bug. 這篇文章主要介紹基本的 assert 語句以及 python 中的unit test 庫。

## Assert

`assert`是pyhton中用於做測試的一個函數，測試的時候我們只需把應該為`True`的表達放在 `assert` 後面即可：

```python
assert len("Hi") == 2
```

如果 `assert` 內的判斷式為 `True` 則無事發生，反之，程序會結束執行並且直接報錯 `AssertionError`. 雖然讓我們知道這裡程序出了問題，但帶來的問題是，我們不知道後面的程序是否還有其他問題。

## Unit Test

為了解決上面提到的問題，我們會使用專門做測試的庫，這個庫可以一次性跑多個測試用例，並且可以更直觀呈現哪些測試用例通過，哪些沒有。

`unittest` 是python 中一個常用的單元測試庫。所謂的單元測試就是對軟體中的最小可測試單元進行驗證，例：驗證軟體內某函數運行是否符合預期。例子：

假如這是我們軟體 `calculator.py` 內的某個函數：

```python
def adder(x, y):
  return x+y  
```

那我們的測試代碼就如下：

```python
import unittest
from calculator.py import adder

class TestAdder(unittest.TestCase):
  def test_positive_with_positive(self):
    self.assertEqual(adder(5,3), 8)
  def test_neg_with_neg(self):
    self.assertEqual(adder(-10,-2), -12)
```

每個測試用例都是class下面的一個方法，名字必須以 `_test` 開頭，只有 `_test` 的方法會被當做測試用例。

寫好測試後，我們只需要運行這個程式就能看到測試結果。測試結果由 `.` 和 `F` 組成，一個 `.` 則代表我們通過一個測試用例，`F` 則代表我們沒有通過。

`unittest` 這個庫中還有更多的測試方法，不局限於 `assertEqual`。此外，由於各個測試用例之間都是獨立的，測試不同用例的時候，我們會不停創建新對象，為了避免不必要的代碼，我們可以用 `setUp` 這個方法，他會在運行各個測試用例前運行一次。

例子：沒有使用 `setUp`

```python
import unittest
from sentence import Sentence

class TestSentence(unittest.TestCase):
  def test_str_count(self):
    sentence = Sentence("hello world!")
    self.assertEqual(sentence.str_count(), 12)

  def test_word_count(self):
    sentence = Sentence("hello world!")
    self.assertEqual(sentence.word_count(), 2)

  def test_upper(self):
    sentence = Sentence("hello world!")
    self.assertEqual(sentence.upper(), "HELLO WORLD!")
```

使用了 `setUp`：

```python
import unittest
from sentence import Sentence

class TestSentence(unittest.TestCase):
  def setUp(self):
    self.sentence = Sentence("hello world!")

  def test_str_count(self):
    self.assertEqual(self.sentence.str_count(), 12)

  def test_word_count(self):
    self.assertEqual(self.sentence.word_count(), 2)

  def test_upper(self):
    self.assertEqual(self.sentence.upper(), "HELLO WORLD!")

```

## 更多內容可以參考

- [(推薦) 灣區筆記 - 使用 unittest 對程式進行測試讓程式更加可靠](https://bayareanotes.com/python-unittest/)

- [Python Documentation - unittest](https://docs.python.org/zh-tw/3/library/unittest.html)
- [拾遺](https://blog.tzing.tw/)[- 使用 unittest](https://blog.tzing.tw/posts/python-testing-use-builtin-unittest-19e9cbe4)
