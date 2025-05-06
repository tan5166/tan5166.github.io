---
title: 爬蟲篇 1 —— HTTP 請求與回應
date: 2025-05-06 16:02:10 +0800
categories: [Data, Web Scraping]
tags: [data, requests, web scraping]     # TAG names should always be lowercase
math: false
---

我們在瀏覽器中輸入地址後，瀏覽器便會向服務器發送 HTTP 請求。HTTP 請求實際上有多種不同的方法，其中較為常見的是，GET 和 POST。

- GET 主要用於獲得數據。當我們瀏覽一個網頁時，瀏覽器會發送 GET 請求來向伺服器索取該頁面的內容，例如文字、圖片、樣式等。GET 請求會將參數附加在 URL 中，因此不適合傳送敏感資訊。
- POST主要用於傳送資料或建立資料。例如當我們在網站上填寫登入表單、留言或註冊帳號，這些動作通常會觸發 POST 請求，將表單中的資訊（如帳號、密碼）傳送到伺服器。這類資料會包含在請求的主體（body）中，不會直接顯示在網址上。



### HTTP 請求

一個完整的HTTP請求如下：

```
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)
Accept: text/html,application/xhtml+xml
Accept-Language: zh-TW
Connection: keep-alive
```

- `GET /index.html HTTP/1.1`：這行指定了請求的資源（index.html），以及使用的 HTTP 協議版本。

- `Host`：告訴伺服器你想連接的是哪個網站（尤其當一個伺服器上有多個網站時）。

- `User-Agent`：標示使用者的瀏覽器與作業系統資訊。

- `Accept`、`Accept-Language`：表示客戶端希望接收什麼格式與語言的內容。

- `Connection`：控制連線是否保持開啟。



## HTTP 回應

在服務器接到 HTTP 請求會返回對應的 HTTP 回應：

```
HTTP/1.1 200 OK
Date: Tue, 06 May 2025 09:00:00 GMT
Server: Apache/2.4.41 (Ubuntu)
Content-Type: text/html; charset=UTF-8
Content-Length: 3056

<!DOCTYPE html>
<html>
  <head>
    <title>Welcome</title>
  </head>
  <body>
    <h1>Hello, world!</h1>
    ...
  </body>
</html>

```

**說明：**

- `HTTP/1.1 200 OK`：表示請求成功（200 是常見的成功狀態碼）。
- `Date`、`Server`：提供回應時間與伺服器資訊。
- `Content-Type`：告訴瀏覽器這是 HTML 文字內容。
- `Content-Length`：內容長度（單位為位元組）。
- 後面就是實際的 HTML 頁面內容。



### 狀態碼

其中在這裡看到的 `200` 為狀態碼，意義如下：

| 類別代碼 | 類別名稱                   | 說明                                     |
| -------- | -------------------------- | ---------------------------------------- |
| 1xx      | 資訊回應（Informational）  | 表示請求已被接收，繼續處理中             |
| 2xx      | 成功（Success）            | 表示請求成功接收並處理完成               |
| 3xx      | 重定向（Redirection）      | 表示需要進一步操作才能完成請求（如跳轉） |
| 4xx      | 用戶端錯誤（Client Error） | 表示請求有錯，可能是語法錯或找不到資源   |
| 5xx      | 伺服器錯誤（Server Error） | 表示伺服器處理請求時發生錯誤             |

簡單來說：

- `2xx` 通常是你希望看到的。

- `3xx` 表示需要跟著跳轉。

- `4xx` 大多是使用者問題（如打錯網址、未登入）。

- `5xx` 則是網站伺服器出包。

