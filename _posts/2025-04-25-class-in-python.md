---
title: Python 中的 Class 和 Class Inheritance 語法
date: 2025-04-25 02:28:00 +0800
categories: [Python, Basics]  
tags: [oop]     # TAG names should always be lowercase
math: false
---

# Class in Python
類（Class）是面向對象編程（OOP, Object-Oriented Programming）的基石。所謂的**面對對象**的意思就是，我們把現實當中的事物抽象成程式中的**對象**（Object），而類就是用來定義這些對象的模版。這樣說可能有點抽象，舉個例子，狗就是一個類，他有 name, age 等屬性，而小黑這條特定的狗就是一個對象，他有屬於自己的名字和年齡。以下是 Python 中類的語法：

```python
# 1. 定義類
class Dog:
    def __init__(self, name, age):
        self.name = name  # 屬性
        self.age = age

    def bark(self):  # 方法
        print(f"{self.name}：汪汪！")

# 2. 建立對象
my_dog = Dog("小黑", 3)

# 3. 使用對象
print(my_dog.name)  # 讀取屬性
my_dog.bark()       # 呼叫方法
```

# Class inheritance in Python
為了更好地貫徹 DRY (Dont Repeat Yourself) 原則，減少重複的代碼，類可以繼承 (inheritance). 繼承指的是「子類別」可以繼承「父類別」的**屬性**和**方法**。比方說「貓」和「狗」都是「動物」的一種，它們都會「吃東西」，但叫聲不一樣。我們就可以先寫一個動物的類，裡面有吃東西的方法，再讓貓和狗的類各自繼承。Python 中的語法如下：
```python
class Animal:
    def __init__(self, name):
        self.name = name

    def eat(self):
        print(f"{self.name} 正在吃東西")

    def speak(self):
        print(f"{self.name} 發出了一個聲音")

class Dog(Animal):
    def __init__(self, name, breed):
        # 呼叫父類別的 __init__，設置 name
        super().__init__(name)
        self.breed = breed
        print(f"Dog: 品種是 {self.breed}")

    def speak(self):
        super().speak()  # 可選：先呼叫父類別的 speak（看你要不要）
        print(f"{self.name}：汪汪！")


class Cat(Animal):
    def __init__(self, name, color):
        super().__init__(name)
        self.color = color
        print(f"Cat: 顏色是 {self.color}")

    def speak(self):
        print(f"{self.name}：喵～")
        
# 使用範例
dog = Dog("小黑", "拉布拉多")
cat = Cat("小花", "白色")

dog.eat()
dog.speak()

cat.eat()
cat.speak()
```

> `super` 可以幫我們呼叫父類裡面的方法。
