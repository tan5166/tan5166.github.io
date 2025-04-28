---
title: Python 中的文件操作
date: 2025-04-25 03:05:00 +0800
categories: [Python, Python Basics]  
tags: []     # TAG names should always be lowercase
math: false
---

## 文件操作
在寫程式的過程中，我們不免需要對文件內容進行操作，例如，我們想把內容寫入文件，又或者我們想讀取文件中的內容。Python 提供一些函數對文件進行操作。

## 打開文件
文件打開有兩種用途，寫和讀。Python 中是這樣打開文件的：
```python
# 根據用途，傳入 r 為 read, w 為 write
open("file_path", "r", encoding="utf-8")
```

### 讀取文件
在打開文件之後，讀取就十分簡單：
```python
f = open("file_path", "r", encoding="utf-8")
print(f.read()) # 讀取全部內容，並打印
print(f.read()) # 讀到空字串，並打印
```
`read` 的時候會記錄讀到的位置，所以第二次 `read` 只會返回空字串。如果文件太大，記得不要一次性 `read` 完整個文件，因為這樣會導致內存爆炸，這時可以 `read(number)` 表示讀取 `number` 個字節的內容。

此外，我們還可以用 `readline()` 來讀取文件，他會一次只讀取一行的內容。我們還有 `readlines()` 這個方法，他會讀取整個文件的內容，並且返回由每行內容組成的 list.

### 寫入文件
寫入文件的方法也很簡單，只需要調用 `f.write(內容)` 就好，就能把內容寫入文件當中。但要注意，如果以 `w` 打開文件，則會清空所有過去內容，寫入你的句子。例子：
```python
f = open("file_path", "w", encoding="utf-8")
f.write("Hello world!")
f.close()
# 此時文件內容為 Hello world!

f = open("file_path", "w", encoding="utf-8")
f.write("HI")
f.close()
# 此時文件內容僅有 HI!
```

如果想追加額外內容而不是覆蓋，請使用 `a` 來打開文件。
```python
f = open("file_path", "a", encoding="utf-8")
```

如果傳入文件名不存在，`w` 和 `a` 模式都會幫我們創建一個，`r` 模式則會報錯。

### `r+` 模式
如果希望同時讀寫，用 `r+` 模式。`r+` 的意思是，**讀取 + 寫入**，不會清空整個檔案，但**寫下去的位置會從檔案的開頭開始覆蓋**。

如果你寫入的字數比原本少，**剩下的原本內容會保留**。如果你寫入的字數比原本多，**只會覆蓋已有的部份，不會自動刪掉多餘的原內容**。

如果希望在讀取之後，從特定位置開始寫入可以用以下方法：
```python
f = open("file_path", "r+", encoding="utf-8")
f.seek(5)  # 把指標移到第5個字
f.write("HAHA")
f.close()
```
如果希望寫入在最後，可以先 `read` 了再寫入。

### 小結

| 模式 | 意思 | 是否清空文件 | 是否從開頭寫入 |
| ---- | ---- | ------------ | -------------- |
| `r+` | 讀寫 | ❌ 不清空     | ✅ 從開頭寫     |
| `w`  | 寫入 | ✅ 打開就清空 | ✅ 從開頭寫     |
| `a`  | 附加 | ❌ 不清空     | ❌ 從結尾寫     |


## 關閉文件
當使用完文件後，記得關閉，才能避免**資源浪費或檔案損壞**。語法是：`f.close()`. 我們還有更加安全的寫法，如下：
```python
with open("test.txt", "w") as f:
    f.write("Hello, world!")
# 出了 with 區塊後，自動 f.close()
```


