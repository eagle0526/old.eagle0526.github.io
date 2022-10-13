---
title: ASTRO Camp Day5 - JavaScript(01)
author: YeeChen
date: 2022-10-07
category: JavaScript
layout: post
---

JS正式開始前言
------

### 前端工程師

html結構、css樣式、JavaScript行為


### JavaScript 跟 Java 的關係

JS當初取名的來由，是去蹭Java名字的熱度(當初Java很紅)，除此之外都沒啥關係


### JavaScript 跟 ES6 的關係
 - ECMA       - 歐洲電腦製造商協會
 - TC39       - 第39號委員會，負責JS的標準化
 - ECMA-262   - JS的規格
 - ECMAScript - 根據ECMA262規範所設計出來的程式語言規則
 - JS         - 某一款符合ECMAScript 的程式語言
 - ES6        - ECMAScript 第六代


### 為什麼不學最新版本就好

瀏覽器跟不上


### NODE.JS
rumtime 執行環境 (這個程式語言可以在哪些環境執行)


> JS
> - 瀏覽器  
> - Node  
> - Deno  
>  
>  上面三個是 JS 的一種 runtime (執行環境)
{: .block-tip}


JS 推薦外掛
 - Babel JS - 如果語法寫對，幫助 hightlighting 語法
 - Prettier - 幫忙排列程式碼
 - Material Icon Theme - 根據你的檔案類型，在檔案左邊給相對 Icon
 - Live Server


***


JS 的 hello world
------

```markdown
> console.log("hi, world");
>
```



### HTML連結 JS檔案

```markdown
 > <script src="file1.js"></script>
 ```


### alert、confirm

```markdown
> alert(" don't touch me ")   -> 彈出警告視窗
>
> confirm(" are u sure? ")   -> 彈出建議視窗
```

***


變數、常數
------

變數就像一個標籤，標籤裡面有很多內容物，想要拿出內容物的時候，就去呼叫他

```markdown
 > 宣告 variable
 > var a = 2;
 >     | a = 變數名字
 >     | = assign 指定的意思
 >     | 2 是值
```



### 變數設定要注意

> 1、不能用數字開頭的字  
> 2、不能用保留字 - 看起來像語法的字 ex. var if = 2  
> 3、注意大小寫有差別  
>
{: .block-warning}




### 未定義undefined vs 沒有定義not define

> 這兩個是有差異的  
> var a;   console.log(a)   -> undefined  
>          console.log(b)   -> not define  
>   
> Ps. undefined 是一個值，not define 就只是純粹啥都沒有  
{: .block-tip}




### 變數如果還沒宣告就拿來用

```markdown
> console.log(a);    -> 會印出undefined  
> var a = 1;
> 
> 這是JS的機制，叫做
> **變數提升 variable hoisting**
> 
> 但是這個很不妙，會造成很多意外
> 
> console.log(b)     -> 會印出not define
> b = 1
```



### let 設定變數

```markdown
> var a = 1;  
> let b = 2;  
> 兩個看起來都一樣  
> 
> 
> **不過如果今天用 let ，可以直接解決變數提升的問題**
> console.log(a)     -> 會印出not define  
> let a = 1  
```



### const 設定常數


假如今天跟別人一起協作，有某個數值你不想被更改，你就可以設定常數

```markdown
> const a = 1
> a = 2;
>
> console.log(a);      -> 印出 Assignment to constant variable.
> Ps.常數不可更改
>
>
> **const 的定義不是不能修改，是不能re assign**
> 
> 如果今天
> const a = ["a","b","c"]
> 
> 情境一
> a[0] = 123
> console.log(a)              -> 會印出 [123, "b", "c"] (可以修改裡面的值)
> 
> 情境二
> a = ["c", "d", "e"]         -> 會印出 Assignment to constant variable.（不能重新指派）
> console.log(a)
> 
```

### const vs. let vs. var
> -  
> 1、寫JS 選擇上使用順序 const > let > var  
> 2、var也可以用，不過範圍大了一點  
> 3、千萬不要沒宣告就使用，會造成很多全域污染  
>
> const 和 let與var的差異是，const是用來設定常數的(不可re-assign)  
> 而 let 和 var 的差異是，var因為設計漏洞的關係，會造成 **變數提升**  
> 發生變數提升會讓後指派的 var 變數，console出來會變成 undefined，而不是not defined  
>
> ex. console.log(a);   # undefined  
>     var a = 1;  
>
> **undefine 和 not define 的差異在於，undefined是一個值，not define是啥都沒有**  
> 而let就是解決變數提升的問題  
>  
> ex. console.log(b);    # not define  
>     let b = 1;  
> -  
{: .block-warning}



a++ vs ++a
------

```markdown
> var a = 1
> console.log(a++)        # 1   -> 先印出a，再執行++
> console.log(a)          # 2   
> 
> var b = 1
> console.log(++b)        # 2   -> 先執行++，再印出b
> console.log(b)          # 2
```

***

原始型別 vs 物件型別
------

#### 原始型別  
數字、字串、真假值、之類的  

#### 物件型別  
大括號、中括號、函數、物件之類的


#### 為什麼要有不同型別
為了不同型別之間的搭配使用  
```markdown
ex. console.log(1+2)  
    console.log("a"+"b")  
```



### 字串顯示


```markdown
> let num = 123  
>   
> console.log("aaa")           # aaa  
> console.log('aaa')           # aaa  
> console.log(`aa${num}a`)     # aa123a -> 這種顯示方式可以塞變數在裡面  
>
> console.log(`she said: "hi"`)# she said: "hi" -> 要在字串裡顯示""，要記得用``  
> console.log(" she said: \"hi\" ")                或是用跳脫字元\  
```


### 改變型別、確認型別

typeof 運算子會傳回一個字串值, 指出未經運算 (unevaluated) 的運算元所代表的型別。


```markdown
> let a = 2;  
> console.log(typeof a)          #Number  
>   
> let b = String(b)  
> console.log(typeof b)          #String  
>
> console.log(typeof(typeof(a))) #String -> 真實樣式是這樣 typeof(Number)
>
```


### NaN介紹 - NaN = Not a Number

```markdown
> console.log(2/"c")               #NaN
> 
> console.log(typeof NaN);         #number  -> NaN是一個數字，不過他代表不是數字  
>                                              就像Null他存在，不過他代表不存在  
>  
> console.log(NaN === NaN);        #false   -> JS唯一一個自己不等於自己的
```

***

流程控制 Flow Control
------

```markdown
> let age = 20  
> if (age >= 18) {  
>  console.log("已成年"`)      
> } else if ( age > 10 && age < 18 ) {        # &&而且、||或  
>  console.log("青少年")  
> } else {  
>   console.log("未成年")     
> }  
>
```

### 三元運算子


```markdown
> age >= 18 ? console.log("已成年") : console.log("未成年")
> 判斷age是否大於18歲，如果成立 "已成年" 否則 "未成年"
> 
> 
> let result = age >= 18 ? "已成年" : "未成年"
> console.log(result)                          #另一種三元運算子


> 三元運算子巢狀表示法
> if (a>1) {
> 
>   if (b>2) {
>       // A
>    } else {
>        // B
>    }
>   else {
>    // c
>   } 
>
> }
> 
> 
> 三元運算子呈現 -> (a>1) ? (b>2) ? A : B : c
```


### 一些意外情況 -> falsy 比較
```markdown 
> var age = 16
> if (age = 20) {               # 如果這邊是用= ， 這塊會變成True
>     console.log("成年")        # 成年 -> 這一串結果會印出成年
> } else {
>     console.log("未成年")
> }
> 
```
[falsy表](https://developer.mozilla.org/en-US/docs/Glossary/Falsy)

***


### switch - if else另外一種寫法


```markdown
> let gender = 0
> switch(gender) {
>     case 1:
>         console.log(1);
>         break;
> 
>     case 2:
>         console.log(2);
>         break
> 
>     default:
>         console.log(3);         # 3  -> 因為gender值為0，因此印出預設值
>         break
> }
```


### for迴圈 


**for(起始值; 滿足條件; 每回合做的事情)**

```markdown
> for (var a = 0; a < 10; a = a + 1) {  
>    console.log(a);                    # 0~9  -> 印出0~9的數字  
> }  
>   
> 情境題 -> 今天想印出 0~100 的所有奇數  
> for (let n = 0; n<=100; n++) {  
>     if (n % 2 !== 0) {  
>         console.log(n);               # 0~100 的奇數 -> 先用for迴圈設定0~100  
>     }                                   再用if判斷這些數字中哪些是奇數  
> }  
>  
```


### while 迴圈


```markdown
> while (true) {                       # 如果()中為true，就一直做下去  
>     console.log("......")  
> }  
>  
> 情境題 -> 今天想印出 0~100 的所有奇數  
> let n = 0  
>  while (n<=100) {  
>    if (n % 2 !== 0) {  
>        console.log(n);  
>    }  
>    n++  
>  }
>
> 情境題 -> 印出 **你好5、你好3、你好1**
> let n = 5
> 
> while (n >= 0) {
> 
>     if (n%2 !== 0) {
>        console.log(`你好${n}`);
>    }
>    n--
>}
>
```

***


prompt使用
------

prompt("請輸入......")

```markdown
> ##### 判斷是平年還是閏年
>
> 被4整除 閏年   被100整除 平年   被400整除 閏年
>        平年            閏年            平年
>
> let year = Number(prompt("請輸入年份"));
> 
> if (year % 4 === 0 && year % 100 !== 0 || year % 400 === 0 ) {
>     console.log("閏年");
> } else {
>     console.log("平年");
> }
```



