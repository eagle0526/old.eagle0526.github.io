---
title: ASTRO Camp Day5
author: YeeChen
date: 2022-10-07
category: JavaScript
layout: post
---

前端工程師
------
html結構、css樣式、JavaScript行為


JavaScript 跟 Java 的關係
------
JS當初取名的來由，是去蹭Java名字的熱度(當初Java很紅)


JavaScript 跟 ES6 的關係
------
 - ECMA       - 歐洲電腦製造商協會
 - TC39       - 第39號委員會，負責JS的標準化
 - ECMA-262   - JS的規格
 - ECMAScript - 根據ECMA262規範所設計出來的程式語言規則
 - JS         - 某一款符合ECMAScript 的程式語言
 - ES6        - ECMAScript 第六代


為什麼不學最新版本就好
-----
瀏覽器跟不上


NODE.JS
------
rumtime 執行環境 (我這個程式語言可以在哪些環境執行)


 > JS
 > - 瀏覽器
 > - Node
 > - Deno
 > 上面三個是 JS 的一種 runtime (執行環境)
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
> 
> console.log("hi");
>
```



js 從 html 檔案連過去
------
```markdown
 >  
 > <script src="file1.js"></script>
 >  
 ```

***

JS 語法
------

```markdown
>
> alert(" don't touch me ")   -> 彈出警告視窗
>
> confirm(" are u sure? ")   -> 彈出建議視窗
> 
```

***


變數、常數
------

變數就像一個標籤，標籤裡面有很多內容物，想要拿出內容物的時候，就去呼叫他

```markdown
 > 
 > 宣告 variable
 > var a = 2;
 >     | a = 變數名字
 >     | = assign 指定的意思
 >     | 2 是值
```



>
> **變數設定要注意**
> 不能用數字開頭的字
> 不能用保留字 - 看起來像語法的字 ex. var if = 2
> 注意大小寫有差別
>
{: .block-warning}




> 未定義undefined vs 沒有定義not define
> 
> 這兩個是有差異的
> var a;   console.log(a)   -> undefined
>          console.log(b)   -> not define
> 
> Ps. undefined 是一個值，not define 就只是純粹啥都沒有
{: .block-tip}




如果還沒宣告就拿來用
------

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



let 設定變數
------

var a = 1;  
let b = 2;  
兩個看起來都一樣  


**不過如果今天用 let ，可以直接解決變數提升的問題**
console.log(a)     -> 會印出not define  
let a = 1  




const 設定常數
------

假如今天跟別人一起協作，有某個數值你不想被更改，你就可以設定常數

```markdown
>
> const a = 1
> a = 2;
>
> console.log(a);      -> 印出 Assignment to constant variable.
> Ps.常數不可更改
>
>
> ***
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

>   
> **const vs. let vs. var**
>  
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
>
{: .block-warning}



**typeof -> JS確認型別的語法**


原始型別 vs 物件型別
------

**原始型別**  
數字、字串、真假值、之類的  

**物件型別**
大括號、中括號、函數、物件之類的


為什麼要有不同型別
------

為了不同型別之間的搭配使用  
ex. console.log(1+2)  
    console.log("a"+"b")  


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