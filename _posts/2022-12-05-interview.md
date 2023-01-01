---
title: 面試題
author: YeeChen
date: 2022-12-05
category: Rails
layout: post
---



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



物件繼承
------

(1) Q. All objects have prototype?      
Ans. false  
詳解：是所有function都有prototype，所有物件都有的是__proto__    

(2) 箭頭函式沒有prototype

(3) 使用new實體時，在類別裡面呼叫return，會發生啥事

```md
> function Cat(name) {
>     this.name = name
>     return 123             -> 如果今天刻意給實體 return  (正常人不會在這邊return)
> }
> 
> const c = new Cat("cc")    -> 實際上會忽略上面傳下來的123，一樣是傳Cat下來
> console.log(c)             # 印出 Cat { name: 'cc' }
```