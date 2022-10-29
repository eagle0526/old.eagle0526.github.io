---
title: ASTRO Camp Day13 - JavaScript(05)
author: YeeChen
date: 2022-10-20
category: JavaScript
layout: post
---


抓網路資料前要注意的東西
======

資料來源 - API Application Programming Interface




RESTFul
---- 

- REST = 表現層狀態轉換
- 網頁資料取得的幾個動詞，這之後會在提到

如果我的網址的CRUD都符合上述方法，就稱為 符合RESTFul API設計
```markdown
> GET
> POST
> PUT
> PATCH
> DELETE
```

> --  
> PUT 會整筆蓋掉，換新了出來  
> PATCH 不會整筆換掉，是一筆一筆蓋掉  
> --  
{: .block-tip}




資料傳輸格式
------
### XML 
是一種延伸標記語言(跟HTML一樣都是標記語言) - 裡面的標籤可以自己定義，不過也只有你自己看得懂

### CSV 逗號分隔值， 所有資料被逗號分格 ( !==excel檔 )

### json (JavaScript Object Notation)
json - 他跟JS很像的關係，因為他是用JS格式寫出來的 (不過要記得，網路上拿到的東西不是物件或是字串的格式，**都是文字喔**)



AJAX Asynchronous JavaScript And XML
------
- AJAX不是一種技術或語法，而是一種術語
- 什麼是非同步 - 假設今天你傳簡訊給同事，他過一陣子才會回你訊息，這就叫非同步
- JS是一種 **單執行緒** 的程式語言 (一個廚房只有一個廚師)


#### 今天執行AJAX是什麼意思

前面正在執行JS，後面在送資料到你的電腦，也就是在畫面執行時，偷偷送資料進來



AJAX應用
------

1. google map
 --  一開始只能載入一小部分的圖資，在你拖拉畫面的時候，他會一直持續load新圖資進來  
 --  滑鼠移到景點名稱時，才跳出名稱，也是AJAX應用  

2. Fetch/XHR
 -- 網路爬蟲
 -- 抓取別人的Json檔案



同步執行、單執行緒的問題
------

### 同步執行有什麼問題嗎
會比較慢，因為JS是單執行緒，今天載入一張圖片時，如果這張圖片很大，那你要等這張圖片載完，才能做其他事情


### 單執行緒
單執行緒的也就是程式執行時，所跑的程式路徑（處理的東西）是連續順序下來的，必須前面的處理好，後面的才會 執行到。  



使用 XHR (XMLHttpRequest) 寫網路爬蟲
------

- 資料來源 - API Application Programming Interface
- jsonplaceholder這個網站可以加入我的最愛(free fake API)，假的API網站，可以拿來練習


```markdown
> const api = "網址"
> const req = new XMLHttpRequest();
> 
> 
> req.addEventListerer("Load", () => {
>     const posts = JSON.parse(req.responseText)
>     // 處理posts顯示(用json.parse處理這個文字檔)
> 
>     const lists = document.querySelector(".lists") -> 抓li物件
> 
>     posts.forEach((post) => {
>         console.log(post.title)                 // 印出陣列所有的title
>         const el = `<li>${post.title}<li>`      // 增加一段HTML
>         
>         // 把抓出來的title放到li的後面
>         lists.insertAdjacentHTML("beforeend", el)
>     })
> })
> 
> req.open("GET", api)
> req.send()
> 
> #### 上面open不能改POST，取用API的時候。方法對，action錯，還是一樣取不到答案
```

```markdown
> ----reduce寫法----
> 
> const rawData = req.resopnseText
> const posts = JSON.parse(rawData)
> 
> const reslut = posts.reduce((acc, {id, userId, title}) => {
>     return acc + `<li>${id} ${userId} ${title}</li>`
> })
> 
> lists.insertAdjacentHTML("beforeend", result);
> });
> 
> ----reduce寫法----
> 
> 在迴圈外定義一個變數，在裡面一直持續用他，通常有更好的寫法
> 
> 
> 這一段看影片在學習一次1021 11:28
> 學習reduce解法
```



***



fetch寫爬蟲
------
```md
> const api = "網址"
> 
> const api = "https://jsonplaceholder.typicode.com/posts";
> 
> fetch(api).then((e) => {
>     console.log(e.json());       -> 印出 promise
> })

> 所有的promise都可以用 catch or then 街
```




Event loop
------

有另外寫一篇完整的文章



stack VS web api vs queue 瀏覽器真正再執行的細節
------

#### stack
- 瀏覽器堆疊的概念
- 先進後出
- FILO

#### Queue
- 先進先出
- FIFO



### 呼叫堆疊
```markdown
> function a() {
>     b()
> }
> 
> function b() {
>     c()
> }
> 
> function c() {
>     console.log("hi")
> }
> 
> a();
> 
> a() 先執行先疊第一層，再來b()，再來c()
> 結束的時候，c() 先抽出來，再來b()，再來a()
> |            |
> | function c |
> | function b |
> | function a |
> --------------
```

> --  
> **stackvoerflow名稱來源**  
> stack -> stack 是存放執行code的地方  
> overflow -> overflow 是溢滿的意思  
> stackoverflow -> 程式堆疊滿出來  
> --  
{: .block-tip}




- setTimeOut or Fetch 等等需要時間的函數

- 使用的時候，會在webAPI排隊，接著會依照函數的執行順序，進到queue

- queue的特性是先進先出

- stack 裡面的東西要完全結束，Queue執行列裡面的東西才會執行

- function結束時就會離開stack

- webAPI沒有順序問題，把他想像成一個廣場

- 監聽器 addEventListener("click") 會一直待在 webAPI 裡面



vip Queue、normal Queue
------

- vip通道進到stack要看stack是否清空
- 一般通道進到stack，要確認vip是否為空，再確認stack是否為空才能進去

> --  
> **之後再提到，queue也有分VIP、normal**  
> 一般的queue  
> setTimeout  
>   
> vip的queue  
> fetch是vip  
> --  
{: .block-top}


**可以去loupe網站看看+操作**
這一段12:36再聽一次做筆記





async寫法 - await記得要在最外圍加上async
------

```markdown
> async function getPost() {
>     const resp = await fetch(api)
>     const posts = await resp.json()
>     renderPosts(posts)
> }
> 
> getPost()
```


跨來源資源分享 CORS Cross  - 面試會問
------

- 如果對方沒有開 CORS policy 是抓不回來的  
- 如果未來碰到業主網站CORS的問題，打電話叫他們開  
- CORS policy test 可以檢測對方CORS有沒有開

> --  
> **CORS是針對瀏覽器的行為，而不是針對JavaScript**  
> 這個行為就是指，假設你今天想從網頁存取別人的個人資料，會碰到資安問題  
>   
> 如果未來有第二個可以控制瀏覽器的語言，這個語言也會碰到CORS的問題  
> --  
{: .block-tip}



### CORS proxy

1. 另外架一個伺服器 (用ruby node python)，去抓對方網站資料
2. 然後因為伺服器是我們自己的，可以把該伺服器的 CORS 打開
3. 就可以用我們自己的JavaScript把那台伺服器的資料抓過來




實際練習爬蟲 - 抓取youbike資料
------






