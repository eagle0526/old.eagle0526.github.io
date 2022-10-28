---
title: ASTRO Camp Day17 - JavaScript(07)
author: YeeChen
date: 2022-10-28
category: JavaScript
layout: post
---


續 this
------

### 5. 是否有使用 apply, call, bind

- bind 跟 apply、call 的差異是， bind 會比較晚觸發(你去主動執行的時候才會觸發)

> --  
> #### bind方法  
> 該bind()方法創建一個新函數，在調用該函數時，將其this關鍵字設置為提供的值  
> 並在調用新函數時提供的任何參數之前具有給定的參數序列。  
>   
> #### 回傳值  
> this具有指定值和初始參數（如果提供）的給定函數的副本。  
> --  
{: .block-tip}



```md
> function hi(n, m) {
>     console.log(this)  -> 這個 this 被bind綁著，現在是指向 hero
>     console.log(n, m)  -> # 1, 2
> }
> 
> const hero = {name: "kk"}
> const newhi = hi.bind(hero)
> 
> hero.name = "cc"       -> 因為用 bind，所以可以先更改一些東西，再主動執行新fc 
> newHi(1, 2)            -> 主動呼叫newHifc
> 
```


> --  
> **bind的好處在哪**  
> bind 會比較晚觸發(你去主動執行的時候才會觸發)  
> 在觸發前，可以更改一些值，改完後在觸發  
> --  
{: .block-tip}


### 6. 是否為嚴格模式 use strict
```md
> function hi() {
>     `use strict`
>     console.log(this) -> undefined
> }
```
不是嚴格模式的情況下，在 fc 裡面使用this，會變成全域變數，嚴格模式下會變成undefined



> --  
> **this 先後順序**  
> 1. 是否為嚴格模式 use strict  
> 2. 是否有使用 new  
> 3. 是否有使用 apply, call, bind  
> 4. () => {} 沒有自己的 this  
> 5. 誰呼叫，誰就是 this  
> 6. 沒人呼叫，this -> 全域物件  
>   
> 嚴格模式 > new > apply、call、bind > 箭頭函式 > 誰呼叫誰就是this > 沒人呼叫為全域物件  
>   
> --  
{: .block-tip}



#### 箭頭函式沒有this，那我們對一個箭頭函式 new 物件會發生什麼事
```markdown
> 會報錯 -> not a constructor
> 
> cosnt heroCreator = () => {}
> 
> const h1 = new heroCreator()
> console.log(h1)
```



> --  
> **箭頭函式缺少的東西**  
> - 缺少this  
> - 缺少一般fc有的arguments  
>   
> 一般函式有一個隱藏 的arguments(引數)  
> ps. 隨便做一個正常的fc -> console.log(arguments)  
>   
> --  
{: .block-tip}





### Cloure 閉包 - 以 setTimeout 舉例

10-28
11.12 -> 修改筆記
非同步回調的問題
for(var i = 0; i < 3; i++) {
    setTimeout(function() => {
        console.log(i)
    }, 1000 * i)
}


let 離開 for 迴圈就會失去作用
var 會一直作用
所以


把上面 for 迴圈中的 var 改成 let 會正常運作 
為什麼改成 let 就可以執行，是因為閉包的概念
var的話就算離開for迴圈還可以存活
所以最後 i 就會讀取 迴圈最後結束的值

如果改成let的話，離開迴圈就無法存活，所以會有一個閉包把這個i一起包進webAPI
之後 setToimeout 的 i 就會依照閉包中的i給值




### Closure 閉包 - fc 都會有這個特性
JS再執行的過程中，會去考慮非同步相關的參數 or function，是否有用for迴圈包住，用let宣告的話，裡面的 i 會持續變動

let原本只會存活在for回圈裡面，但是被setTimeout一起帶去webAPI裡面，所以等 stack 裡面全部執行完後， let才會依然存活

他會去捕捉周圍的環境變數，但是只會去抓字幾有用到的東西
ex. 下面筆記補上


10-28
11.22分
有一個fc的範例，筆記要補做


return hey 的時候，會做一個閉包把要用的參數傳出去




斐波那契數列
------

前兩個位數的數字相加 = 新的位數數字

```md
> function fib(n) {
>     if( n === 0 ) {               -> 到0停止
>         return 0
>     }
> 
>     if (n===1) {
>         return 1
>     }
> 
>     return fib(n-1) + fib(n-2)    -> 可以自己呼叫自己的原因，是因為有終止條件
> }
> 
> console.log(fib(10))
```

> --  
> 糖果題今天如果寫得太複雜，可以試試用遞迴方式來寫  
> --
{: .block-warning}



### IIFE = Immediately Invoked Function Expression (念 " 一 ㄈㄧ " )

寫套件的時候很常用到，因為不想讓自己的套件的fc被影響到
```md
> 用一個小括弧把fc包住，並在最後用()呼叫此fc
> (function () {
>     console.log("123")
> })**()**;              -> 最後記得用()呼叫，可以帶參數進去喔
> 
> 這種寫法的目的，是因為只能使用一次，不會漏到外面
```






























