---
title: ASTRO Camp Day8 - JavaScript(02)
author: YeeChen
date: 2022-10-13
category: JavaScript
layout: post
---



函數 function
------

### 什麼是函數？
f(x) = 3x + 2

f -> function的縮寫
x -> 參數 parameter

### 為什麼要寫函式
為一函式定義一個行為


### function helloworld
```markdown
// name -> 參數parameter
function sayMyName(name) {
    console.log("hi222222");
    console.log(name);
}

// "Yeeeeee" -> 引數argument
// () -> 呼叫、使用、啟動
sayMyName("Yeeeeee")
```



#### 如果函數有一個參數，但是如果飲用的時候啥都沒給，最後會給你undefined
```markdown
function sayHi(name) {
    console.log(name)
}

sayHi()                              -> undefined
```


#### 參數給一個，引數給兩個，最後會給你第一個
```markdown
function sayHi(name) {
    console.log(name)
}

sayHi(1, 2)                         -> 1
```

#### 幫某個參數設定預設值
```javascript
function sayHi(name, age = 18) {    -> 預設為18
    console.log(name)
    console.log(age)
}

sayHi("kk")                         ->  印出"kk"、18
```


### 匿名函數anonymous

常數設定 + 函數設定融合 (後面function整段叫做匿名函數)

```javascript
const sayMyName = function ccc(name) {    -> 裡面ccc可寫可不寫，因為ccc出function範圍就沒有意義
    console.log(name);
};

隱藏寫法
const sayMyName = function (name) {       -> 裡面ccc可寫可不寫，因為ccc出function範圍就沒有意義
    console.log(name);
};
```

#### 函數定義寫在前面 - 是可以執行的

```javascript

sayHi("kk")                         ->  印出"kk"、18

function sayHi(name, age = 18) {    -> 預設為18
    console.log(name)
    console.log(age)
}


```

#### 變數宣告函數寫在前面 - 無法執行(會噴出ReferenceError)

```javascript
say("kk")                         ->  噴錯 ReferenceError

let say = function sayHi(name, age = 18) {
        console.log(name)
        console.log(age)
}
```

> ---  
> undefined() 呼叫，會造成typeErroe
> ---
{: .block-tip}

### 變數提升

#### 宣告的時候發生了什麼事

**JS分兩階段運作**
 - 第一輪是掃瞄 - 建立期
  - 1A - 註冊名稱(identifier)
  - 1B - 進行初始化(檢查語法、建立變數) 
 - 第二輪式執行 - 執行期
  - 執行函數、賦值

```markdown
> 情境算式
> var a = 1
> console.log(a)
>
> ----------
> 建立期
> var a        1A、1b
> 
> 執行期
> a = 1           2
> console.log(a)  2
```
> --  
> 兩階段運作  
> 建立期間把所有程式碼掃過，並把名稱都設定好  
> 執行期間才把值給出去  
> --  
{: .block-warning}

#### 如果把宣告寫在log下方

```markdown
> 情境算式
> console.log(a)
> var a = 1
>
> ------ 
> 第一階段
> console.log(a)     # 不執行
> var a = 1          # 執行 1A、1B -> 已初始化，但是還沒賦值
> 
> 第二階段
> console.log(a)     # 執行，印出undefined
> var a = 1
```


```markdown
> 情境算式
> var a = 1
> var a
> 
> console.log(a)   -> 1
> 
> --------
> 第一階段
> var a = 1              # 執行 undefined
> var a                  # 執行 undefined
> 
> console.log(a)         # 不執行
> 
> 
> 
> 第二階段
> var a = 1              # 執行，給值變1
> var a                  # 執行，但是啥都沒給，所以忽略
> 
> console.log(a)         # 執行，印出a是1
``` 

```markdown
> 情境算式
> if (false) {
>     var a = 1
> }
> console.log(a)    -> undefined
>
> ---------
> 第一階段
> if (false) {                      # 沒執行
>     var a = 1                     # a = undefined
> }
> 
> console.log(a)    -> undefined    # 沒執行
> 
> 
> 第二階段
> if (false) {                      # 執行
>     var a = 1                     # 因為if裡面是false 所以不執行
> }
> 
> console.log(a)    -> undefined    # 執行，最後印出undefined
```


### let 怎麼解決變數提升 - 1b不執行

```markdown
> 第一階段
> console.log(a)     # 不執行
> let a = 1          # 不執行1b, 被一個罩子蓋住了(TDZ)
> 
> 第二階段
> console.log(a)     # 執行, 但是因為，1b沒執行，噴出referenceError
```

#### TDZ暫時死區 Temporal Dead Zone
給值的話，蓋子就會被拿開


```javascript
> **正常情況 let 的執行狀況**

第一階段
let a = 1          # 執行，不執行1B，並給一個蓋子
console.log(a)     # 不執行

第二階段
let a = 1          # 執行，把蓋子拿掉
console.log(a)     # 執行，印出 a = 1
```


#### JS執行function的順序
```javascript
第一階段
sayHi()                   # 不執行
function sayHi() {        # 執行 - sayHi執行1a、1b   {}執行2 
    console.log()
}

第二階段
sayHi()                   # 執行
```

=> 因爲第一階段{}會執行2(執行函數賦值)，因此第二階段執行的時候，才可以成功執行




### 什麼是scope


var = function scope  
let/const = block scope  

var 會被 function 包住，但是無法被 {}block包住   
let/const 只要有一個大括號就可以把他包住  


#### 情境題
```javascript
var age = 20
if (age >= 18) {
    const message = "未成年"
} else {
    const message = "已成年"
}

console.log(message) -> 因為const被{}包住，所以噴會出is not defined
```