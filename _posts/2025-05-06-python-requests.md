---
title: 爬蟲篇 2 —— Python requests
date: 2025-05-06 16:09:28 +0800
categories: [Data, Web Scraping]
tags: [data, requests, web scraping]     # TAG names should always be lowercase
math: false
---

`requests` 是 Python 中非常常用的 HTTP 請求庫，能幫助我們以簡潔的方式發送 GET 或 POST 請求，是進行網頁爬蟲時的核心工具之一。

## 安裝 requests

在命令提示字元（CMD）中輸入以下指令安裝：

```bash
pip install requests
```



## 發送 GET 請求

我們可以用下列方式向網站發送一個 GET 請求：

```python
import requests

url = "http://www.example.com"  # 注意要加上 http:// 或 https://

response = requests.get(url)
```



## 檢查回應狀態碼

你可以用 `response.status_code` 來檢查是否成功：

```python
if response.ok:
    print("請求成功！")
    print(response.text)
else:
    print(f"請求失敗，狀態碼：{response.status_code}")
```



## 加入 headers

### 為什麼要加入 headers？

在實際爬蟲過程中，有些網站會檢查請求的「身份」，以判斷是不是由瀏覽器發出的正常訪問。如果使用程式發送請求而沒加上適當的 headers，網站可能會拒絕回應或直接返回錯誤頁面。

當我們用瀏覽器上網時，瀏覽器會自動加上一些請求標頭（headers），例如 `User-Agent`，它能告訴伺服器「我是用 Chrome/Firefox 發出的請求」。
 但用 `requests.get()` 預設沒有這些 headers，網站就會懷疑這是機器人，進而封鎖或返回錯誤頁。

為了讓請求更像「真人操作」，我們通常會自己加入常見的 headers。

### 範例：加入 User-Agent

```python
import requests

url = "http://www.example.com"

headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36"
}

response = requests.get(url, headers=headers)

if response.ok:
    print("請求成功！")
    print(response.text)
else:
    print(f"請求失敗，狀態碼：{response.status_code}")
```



### 其他常見 headers（可視情況加入）

```python
headers = {
    "User-Agent": "Mozilla/5.0",
    "Accept-Language": "zh-TW,zh;q=0.9",
    "Referer": "https://www.google.com"
}
```

這樣可以模仿「正常使用者點進網站」的情境，增加成功取得資料的機率。



