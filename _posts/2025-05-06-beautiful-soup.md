---
title: 爬蟲篇 3 —— 用 Beautiful Soup 解析 HTML
date: 2025-05-06 17:38:37 +0800
categories: [Data, Web Scraping]
tags: [data, requests, web scraping]  # TAG names should always be lowercase
math: false
---

雖然 `requests` 可以抓取網頁內容，但拿到的只是一整包 HTML 原始碼，我們還需要一個工具來「解析」這些標籤，才能準確找到我們要的資料（像是文章標題、表格內容、圖片網址等等）。而 Beautiful Soup 就是這樣的一個工具。



## 安裝 BeautifulSoup

```bash
pip install beautifulsoup4
```



## 如何使用

以下透過一個簡單的例子，來搭配上 `requests` 抓取頁面並且打印出標題：

```python
import requests
from bs4 import BeautifulSoup

url = "https://example.com"
res = requests.get(url)
soup = BeautifulSoup(res.text, "html.parser") 

print(soup.title.text)
```



## 常用功能

接下來我們介紹一些常用的功能：

### 找標籤

```python
soup.find("h1")         # 找第一個 h1
soup.find_all("p", attrs = {"class": "price_color"})      # 找所有段落, 並且class 是 price_color, 適用於多項篩選
```



### 用 class 或 id 選擇

```python
soup.find("div", class_="news") 
soup.find(id="main")
```



### 抓取內容與屬性

```py
img = soup.find("img")
print(img["src"])       # 抓圖片網址
print(img.get("alt"))   # 抓圖片說明文字
```



在找到對應的標籤後，我們可以通過`.string` 的方法把他們轉為 string, 而不打印標籤。以下是一個範例碼，用於獲取網站上的全部價格：

```python
import requests
from bs4 import BeautifulSoup

url = "https://books.toscrape.com/"

headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36"
}

response = requests.get(url, headers = headers)
print(response)

if response.ok:
    print("Success!")
    content = response.text
else:
    print("Fail")

soup = BeautifulSoup(content, "html.parser")

all_prices = soup.find_all("p", class_= "price_color")

for price in all_prices:
    print(price.string[2:])
```

