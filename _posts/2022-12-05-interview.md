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
