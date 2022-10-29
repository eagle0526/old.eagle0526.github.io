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
> 該bind()方法創建一個新函式，該函式被呼叫時，會將 this 關鍵字設為給定的參數，並在呼叫時，帶有提供之前給定順序的參數。
>   
> #### 回傳值  
> 他會回傳一個新的 fc，並且會把傳進去的東西東做this的初始值
> --  
{: .block-tip}



#### bind舉個例子更好懂 - fc舉例

先給一個fc，印出this
```md
function hi() {
    console.log(this)   -> 這個this是全域變數
}

hi()
```

創建一個新變數，並用hi.bind([])會發生什麼事
```md
function hi() {
    console.log(this)   # [Number: 123]    -> 這個this是bind傳進來的數字 
}

const newHi = hi.bind(123)    -> 這個 newHi 因為 bind 的關係，是一個fc
```

也因為newHi是一個新的fc，所以在主動呼叫之前，他不會發動
```md
newHi()   -> 主動發動
```

#### bind舉個例子更好懂 - 物件舉例

剛剛只有fc和123可能不太好懂，我們今天加入物件試試  
  
創建一個ironMan物件
```md
const ironMan = {name: "ironMan"}
```

把這個ironMan換成剛剛bind裡面的123
```md
const newHi = hi.bind(ironMan)
```

這時候呼叫newHi，就會跑出ironMan物件了
```md
newHi()         # {name: "ironMan"}

ps. 會印出來是因為前面的hi()，我有寫console.log(this)喔！不要忘記
```
  
  
**不過目前還看不出好處在哪對不對，我把整段code更改一下**
```md
1. 一樣給一個fc，然後帶兩個參數
function hello(n, m) {
    console.log(this)    # {name: "ironMan"}  -> 在fc執行前，物件被修改了
    console.log(n, m)    # (1, 2)             -> fc 可以帶參數進來
}
  
2. 一樣有一個ironMan物件
const ironMan = {name: "ironMan"}
  
3. 一樣用bind做出一個新物件，並帶入ironMan
const newHello = hello.bind(ironMan)
  
4. **不一樣的來了，我們在執行前，先改變 ironMan 的值**
ironMan.name = "ironHeart"
  
5. 執行，並帶一些參數給newHello
newHello(1, 2)
```
  
> --  
> **bind的好處在哪**  
> bind 會比較晚觸發(你去主動執行的時候才會觸發)  
> 在觸發前，可以更改一些值，改完後在觸發  
> --  
{: .block-tip}
  
  
### 6. 是否為嚴格模式 use strict
不是嚴格模式的情況下，在 fc 裡面使用this，會變成全域變數，嚴格模式下會變成undefined
```md
> function hi() {
>     `use strict`
>     console.log(this) -> undefined
> }
```
  
  
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
> ps. 可以試試做一個正常的fc -> console.log(arguments)  
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






parcel 打包檔案 - parcel是一個上線過程的“打包器”  
------

### 如果今天太多JS、CS檔案，要在index.html連結其他檔案的時候，該怎麼辦？

```md
> 現在有3個js檔案，我想把這三個壓成一個JS檔案 -> webpack、parcel可以做到
> <script src="app.js"></script>
> <script src="test.js"></script>
> <script src="house.js"></script>
```

> --  
> 市面上有很多打包工具，可以把一大堆的JS、css壓縮成一包小東西  
> npm -> 前端世界專門安裝套件的東西 (npm有點慢)  
> yarn -> facebook做的，誕生原因是因為 npm 有點慢  
> ( yarn 比較快的原因，是因為yarn可以平行下載，一次下載多個檔案 )  
> --  
{: .block-tip}


### 實際執行

在專案終端機輸入
```md
> yarn init
```

會誕生一個json檔案 => package.json
```md
> {
>   "name": "day17",
>   "version": "1.0.0",
>   "main": "index.js",
>   "license": "MIT",        -> 此專案的授權來源
> }
```
> --  
> MIT是麻省理工  
> BSD是柏克萊  
> 這兩間授權的話，基本上都可以免費使用  
>   
> GPL也是一種開源的受援，不過你今天用GPL的lincese寫一份專案，你那一份專案也要開源  
> 
> --  
{: .block-tip}



1. 接著在json檔上的scripts加一些code
```md
> scripts -> 這個很常是前端工程師，加入自己很常用的語法

> "scripts": {
>     "hi": "echo 123",
>     "hey": "echo 456"
> }
> 
> 呼叫hey預設方法
> yarn run hey           # 456 
```

2. 安裝 parcle  
```md
> yarn add --dev parcel 

> 輸入後，會直接下載一大堆檔案，包在一個資料夾(node_modules)裡面 
```


並會在json檔生成一個多幾行程式
```md
> "devDependencies": {
> "parcel": "^2.7.0"
> }

> dev是開發的意思 - devDependencies
```


> --  
> 如果不小心刪掉node_modules  
> 再打上yarn install就會回覆   
> --  
{: .block-tip}


3. 接著到.json檔的scripts裡面，新增一段
```md
> 下面這一行的指令，就跟 rails s 一樣，就是啟動server

> "scripts": {
>     "dev": "yarn parcel index.html"  ->  加在這邊的關係，是因為我之後想重複只用 dev 這個指令
> },                                       要注意那個index.html，如果今天沒有把script包在index裡面
>                                          就要yarn parcel src="this_test.js"
```

4. 接著直接呼叫
```md
> yarn run dev
```

如果今天沒有加上dev那一條，可以直接這樣
```md
> yarn run "yarn parcel index.html"
```

5. 最後把type="module" 寫進script裡面
```md
> <script src="app.js" defer type="module"></script>
```

這樣寫後，開啟環境，並開後台會發現 scr: "一長串的姓名.js"  
以前的時代，瀏覽器會進行快取，所以index 有為每個檔案取名一長串得符號，如果內容物改變的話，名字究會改變   



es modules 如果今天想要引用別人的模組 
------

## 引用自己寫的套件

### 模組輸出

現在在math.js
```md
> 輸入給別人用
> export function add(a, b) {
>     return a + b
> }
```

另外一種export寫法
```md
> function add(a, b) {
>     return a + b
> }
> export { add, minus, mmultiple } -> 也可以在最後寫export，把所有想要傳出去的傳出去
```


### 模組輸入

現在在app.js
```md
> 引用別人套件
> import{ add, PI } from "./math.js"  -> 這個add套件是寫在math.js裡面的
>                                     -> 如果今天有多個要import，可以,隔開就好
> console.log(add(1, 5))     # 6
```

> --   
> 如果今天沒有打包模組，系統會看不懂import、export  
> --  
{: .block-warning}


```md
> 這個default是什麼，就是一個預設匯出的東西
> export default add -> export default 只會有一個
> 
> import X from "./math.js"   -> 輸入預設的模組，可以隨便取名使用
```

> --  
> 輸入也可以全部加寫在一起  
> import X, { add, minus } from "./math.js"  
> --  
{: .block-tip}



## 引用別人的套件

```md
> yarn add dayjs -> 這樣會把dayjs裝在node_modules裡面
> 
> import dd from "./dayjs" -> 直接取用就可以，可以隨意取名的原因，是因為對方的fc是default
```


如果匯入同個資料夾有相同的fc，再匯入的時候，記得用as
```md
> import { add as myAdd } from "./math.js" 
> 
> function add() {
>     console.log(234)
> }
```





























