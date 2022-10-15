---
title: ASTRO Camp Day9 - JavaScript(03)
author: YeeChen
date: 2022-10-14
category: JavaScript
layout: post
---

陣列 - 續
------

### slice語法
slice() 方法會回傳一個新陣列物件，為原陣列選擇之 begin 至 end（不含 end）部分的淺拷貝（shallow copy）。而原本的陣列將不會被修改。

```markdown
> const list = ["a", "b", "c", "d"]
> cost hi = list;
> hi[0] ="x"                       -> 這樣兩個印出來，都會兩個都會改到
> 
> console.log(list)               # ["x", "b", "c", "d"]
> console.log(hi)                 # ["x", "b", "c", "d"]
```

### slice 複製一個陣列
如果今天想要一個新的陣列，且不想要影響到原陣列
```markdown
> const list = ["a", "b", "c", "d"]
> cost hi = list.slice()           -> 複製一個陣列出來
> hi[0] ="x"                       -> 這樣兩個印出來，不會影響到list
```




尋找陣列中是否有某元素存在 - 常用
------
### 方法一 : indexOf()
indexOf() = indexOf() 方法會回傳給定元素於陣列中第一個被找到之索引，若不存在於陣列中則回傳 -1。

```markdown
> const list = ["a", "b", "c", "d"]
> console.log(list.indexOf("c"))      # 2
> console.log(list.indexOf("u"))      # -1
```



### 方法二 : incudes()
includes() = includes() 方法會判斷陣列是否包含特定的元素，並以此來回傳 true 或 false。
```markdown
> const list = ["a", "b", "c", "d"]
> console.log(list.indexOf("c"))      # ture
> console.log(list.indexOf("u"))      # false
```



印出陣列中所有元素
------

```markdown
> const list = ["a", "b", "c", "d"]
```

### for迴圈
```markdown
> for(i = 0; i<= lst.length-1; i++) {
>     console.log(lst[i]);
> }
```

### forEach - 遍歷元素
forEach() 方法會將陣列內的每個元素，皆傳入並執行給定的函式一次。

```markdown
> list.forEach((item) => {
>     console.log(item)
> })
```

#### forEach 實戰 - 印出陣列中所有元素類別(typeof)
```markdown
> const lst = [1, "2" ,3 ,"4" ,5]
> lst.forEach((item) => {
>     return console.log(typeof item);             # Number String Number String Number
> })
```


找指定元素 - find方法
------

find = find() 方法會 **回傳第一個** 滿足所提供之測試函式的元素值。否則回傳 undefined。

```markdown
> const list = [1, 2, 3, 4, 5]
> 
> const result = list.find((x)=>{
>     return x > 3;                  # 4
> })
> console.log(result);
```


### 實戰 - 得到大於6的偶數
```markdown
> const lstNum = [1,2,3,4,5,6,7,8,9,10]
> const newLst = lstNum.find((x)=>{
>     return (x > 6 && x % 2 === 0)  ;
> })
> console.log(newLst);
```



### 實戰 - 得到所有偶數

#### forEach方法
```markdown
> const list = [1, 2, 3, 4, 5]
> const result =[];               -> 用 forEach，要先在外部宣告一個變數，這樣裡面取用的時候才能用
> list.forEach((item) => {
>     result.push(item*2)            # [2,4,6,8,10]
> })
```


#### map方法 - 這個好用在會自動產生新陣列
map = map() 方法會建立一個新的陣列，其內容為原陣列的每一個元素經由回呼函式運算後所回傳的結果之集合。

```markdown
> const list = [1, 2, 3, 4, 5]
> const newResult = list.map((item) => {
>     return item * 2;
> })
> 
> console.log(newResult);
```



filter - 單純過濾陣列
------
filter() 方法會建立一個經指定之函式運算後，由原陣列中通過該函式檢驗之元素所構成的新陣列。

```markdown
> const list = [1, 2, 3, 4, 5]
> const newResult = list.filter((item) => {
>     return item > 3;                      # [4, 5]
> })
> 
> console.log(newResult);
```


#### 實戰 - 篩選出陣列中的字串，長度大於3的元素
```markdown
> const list = ["a", "aaaa", "cc", "ccccc", "dddd"];
> 
> const newResult = list.filter((item) => {
>     return item.length > 3;
> })
> 
> console.log(newResult);
```





加總陣列中的元素
------

```markdown
> const list = [1, 2, 3, 4, 5]
```

### forEach 方法
```markdown
> let result = 0;
> list.forEach((item) => {
>     result = result + item
> })
> 
> conosle.log(result)         # 15
```

### reduce
reduce() 方法將一個累加器及陣列中每項元素（由左至右）傳入回呼函式，將陣列化為單一值。

```markdown
> const result = list.reduce((累加值, 目前值) => {
>     return 累加值 + 目前值;
> }, 起始值)
> 
> ----
> 
> const result = list.reduce((x, y) => {
>     return x + y;                 
> }, 0)
> console.log(result)                         # 15
```



#### 用 reduce 取最大值 - 正常不會用這個方法取最大值

用 reduce 的特性，reduce 照著陣列順序 2 個 2 個抓出來，然後用 if 來比較兩個數字
```markdown
> const list = [1, 5, 2, 19, 7, 18]
> const result = list.reduce((acc, cv) => {
>     if (acc > cv) {
>         return acc                           -> 兩兩比較，比較大的值放在累計值
>     } else {
>         return cv                            ->         比較小的值放在目前值
>     }
> })
> 
> console.log(result)                          # 19 -> 最大的值是最後的累計值
```



> --  
> 何謂高階函數 higher-order function  
>  1、可以把 function 當作參數傳入另一個 function  
>  2、可以回傳 function  
>    
> **只要符合上面其中一點，就可以說是高階函數** 
>  
> --  
{: .block-tip}



物件 Object
------

物件 = 一個東西 = 屬性 + 行為

有一個物件 aa   
 - key = a, b, c, attack  
 - value = 123, 333, "ddd", function  
  
```markdown
> const aa = {
>     a: 123,
>     b: 333,    
>     c: "ddd",
>     attack: function() {
>         console.log("hi")
>     }
> }
```


### 拿取key中的值 - 下面兩種方法都可以
```markdown
> console.log(aa["c"])    # ddd
> console.log(aa.c)       # ddd

> 什麼時候只能用[]拿取值 - 變數字數是組合的方式，就一定要用此種方式
> const myKey = "na" + "me"
> console.log(aa["myKey"])
```

### 呼叫物件的function
```markdown
> aa.attack()              # hi
```


### 物件的 CRUD

```markdown
#### C - 新增物件中的值，把key塞進物件中

> aa.test = "fff"         
> console.log(aa)          # { a: 123, b: 333, c: 'ddd', attack: [Function: attack], test: 'fff' }
```

```markdown
#### R - 讀取指定key的value

> console.log(aa.b)        # 333
```

```markdown
#### U - 更新物件的key

> aa.a = "no"
> console.log(aa)          # { a: "no", b: 333, c: 'ddd', attack: [Function: attack], test: 'fff' }
```

```markdown
#### D - 刪除值物件中的值

> delete aa.b;
```

### 如果今天key值是數字，要怎麼取value

```markdown
> const hero = {
>     0: "a",
>     1: "b",
>     2: "c"
> }
> 
> console.log(hero[1])         # b
```

***


DOM 文件物件模型
------

- HTML不是物件，為了方便操作，瀏覽器會根據HTML結構，轉成一個一個物件  
- DOM是瀏覽器把HTML物件化後的結果  
- HTML不是DOM元素  

> --  
> JS 無法直接取用 HTML，中間有一層瀏覽器  
> JS 會操作瀏覽器來更改瀏覽器的介面(但是HTML 的 code 不會被動到)  
> --  
{: .block-tip}




如果有連續id 會抓到第一個
------

```markdown
> 我先給五個同id的div

> <div id="test">1</div>
> <div id="test">2</div>
> <div id="test">3</div>
> <div id="test">4</div>
> <div id="test">5</div>

> 抓 id 為 test 的元素
> const newId = document.querySelector("#test")

> 把剛剛抓到的元素，點到他會印出"123"
> newId.addEventListener("click", () => {
>     console.log("123");
> })

> 這樣最後在瀏覽器那邊會發現，只有點到第一個元素，可以觸發這個console.log
```


> --  
> 如果印出來的結果是 null  
> 有可能是寫在HTML的 script src 寫在太前面  
> 導致物件化過程比較慢  
> --  
{: .block-warning}


```markdown
> 解決方法
> 法一 : 把scrit放在抓取物件的後面
>     <div id="abc">hi</div>
>     <script src="dom.js"></script>


> 法二 : 直接加一個defer
> <script src="dom.js" defer></script>
> 
> defer 是延遲執行的意思，這個加上可以讓JS等HTML執行完再執行
```


***

抓取id的兩種方法
------

先給一個DIV
```HTML
<div id="abc">123</div>
```

並用兩種語法來抓取div的id
```markdown
> #### 舊方法 - getElementById
> const mydiv = document.getElementById("abc")

> #### 新方法 - querySelector
> 這個方法比較好用，因為後面是使用選取器
> const mydiv2 = document.querySelector("#abc");
```



### 實際應用 - 選取器
```markdown
> HTML
> <ul>
>     <li></li>
>     <li></li>   -> 我要抓這個
>     <li></li>
> </ul>
```
```markdown
> 用nth-child來抓指定標籤
> const mydiv2 = document.querySelector("ul li:nth-child(2)");
```

> --  
> 用 querySelector 抓元素，可以用任何 css 選取器的方法  
>   
> --  
{: .block-tip}




### 一次抓取多個元素

先在HTML設定li的class
```markdown
> HTML
> <ul>
>     <li class="list"></li>
>     <li class="list"></li>
>     <li class="list"></li>
> </ul>
```

用兩種方法抓取所有元素
```markdown
> 方法一
> getElementsByClassName
> const lists = document.getElementsByClassName("list")

> console.log(lists)                  # HTMLCollection(3) [li.list, li.list, li.list]
```

```markdown
> 方法二
> querySelectorAll
> const lists2 = document.querySelectorAll(".list")

> console.log(list2)                  # NodeList(3) [li.list, li.list, li.list]
```



### HTMLCollection vs NodeList

兩種抓取ID的方法 - 抓到的東西不同

- getElementsByClassName 抓到的是HTMLCollection，要把裡面東西印出來只能用for迴圈
- querySelectorAll 抓到的是NodeList，可以使用forEach把裡面東西印出來

```markdown  
> #### HTMLCollection  
> getElementsByClassName 抓到的是一個物件，裡面包著所有東西  
> 如果想要把物件裡面的東西印出來，只能用for迴圈印出來  
  
> for(let i = 0; i < oldBlock.length; i++) {
>     console.log(oldBlock[i]);
> }

> 上面的 for迴圈，會把剛剛抓到的區塊，全部印出來
> <li class="list"></li>
> <li class="list"></li>
> <li class="list"></li>
```

```markdown
> #### NodeList - 多了forEach功能  
> querySelectorAll 抓到的是一個物件，也包著所有東西  
> 但是想要把裡面東西抓出來的話，可以用forEach拿法  
 
> newBlock.forEach((item) => {
>     console.log(item);
> })

> 用forEach把內容物全部印出來
> <li class="list"></li>
> <li class="list"></li>
> <li class="list"></li>
```


***



### textContent - 更改文字

剛剛抓到指定元素後，可以使用textContent來更改元素的文字

先設定一個div id
```markdown
> HTML
> <div id="abc">hi</div>
```


```markdown
> javascript
> 抓到 id = "abc" 的 div後
> const mydiv = document.getElementById("abc")

> 把這個物件裡面的值，改成 "aaa"
> mydiv.textContent = "aaa"
```


### 實戰練習 querySelectorAll + textContent

利用 querySelectorAll 一次抓相同class的物件，並用 textContent 更改文字

```markdown
> HTML
> <div class="aa">1</div>
> <div class="aa">2</div>
> <div class="aa">3</div>
> <div class="aa">4</div>
> <div class="aa">5</div>
```


```markdown
> javascript
> #### 使用 forEach + textContent

> sinBlock.forEach((e) => {
>     e.textContent = "帥哥"              # 這可以把HTML的五個div文字都改成帥哥
> })  
```



```markdown
> javascript
> #### 使用 for 迴圈 + textContent

> for(let i = 0; i < sinBlock.length; i++ ) {
>     sinBlock[i].textContent = "帥哥"    # 這可以把HTML的五個div文字都改成帥哥
> }

```


***



### innerHTML - 渲染HTML

```HTML
<div id="test">hi</div>
```

```markdown
> 先抓到 id = test 的 div
> const mydiv = document.querySelector("test")

> 把該元素變成 h1 元素
> mydiv.innerHTML = "<h1>dsf</h1>"
```



### classList 類別元素

用 classList 可以修改抓取元素的 class

```HTML
<style>
    .red {
        font-size: 20px;
        color: red;
    }
    .green {
        font-size: 30px;
        color: green;
    }
</style>
```

```markdown
> 把元素的class，修改class為.red的屬性
> mydiv.classList.add("red")

> 把元素的class，修改class為.green的屬性
> mydiv.classList.add("green")
```




事件監聽器 addEventListener
------

什麼時候會有 **事件** 發生？網頁只要有任何變動，都會有事件發生  
加一個事件監聽器，這個可以解決 script scr 被晚寫的狀況  
為整個網頁會先執行完後，再來執行這些事件  


像下面這樣寫，就可以解決script先後讀取的問題  

```markdown
> 舊寫法 - 使用DOMContentLoaded 
> document.addEventListener("DOMContentLoaded", () => {
>     const mydiv = document.querySelector("#test");
>     mydiv.innerHTML = "<h1>dsf</h1>";
> });
 
> 新寫法 - 加一個difer，讓js晚一點執行 -> 推薦這個
><script src="dom.js" defer></script>
```




### callback function 回呼函數
```markdown
> myDiv.addEventListener("click", (e) => {
>     console.log(123);
>     console.log(e);                     => 這個稱為 callback function
> })

> 上面兩個log分別會印出下面這兩個
> 123
> PointerEvent {isTrusted: true, pointerId: 1, width: 1, height: 1, pressure: 0, …}
```




重複使用監聽元素
------

先設定兩個 div
```HTML
<div id="test">hi</div>
<div id="test2">goodby</div>
```

抓取後，在用addEventListener監聽器，重複觸發中間段設計的監聽函數
```markdown
> const myDiv = document.querySelector("#abc");
> const youDiv = document.querySelector("#xyz);
> 
> const clickHandler = (e) => {
>     console.log(234)
>     console.log(e.target);        -> 可寫可不寫, 這一行只是提醒你 那個 e 會傳下來
> }
> 
> myDiv.addEventListener("click", clickHandler);
> youDiv.addEventListener("click", clickHandler);
```



各自點擊元素後，會印出下面訊息
```markdown
> 點擊 id = "test2" 的div
> byeybe
> <div id="test2">goodby</div>
 
> 點擊 id = "test2" 的div
> byebye
> <div id="test">hi</div>
```




預設行為 - preventDefault
------

很多標籤都有預設行為，像是超連結 or 表單，我們可以利用 preventDefault 來先暫停，這些預設行為
  
  
設定一個a標籤
```HTML
<a href="google.com">Google</a>
```

抓到此標籤後，把a標籤的預設行為關掉
```markdown
> const link = document.querySelector("a")
> 
> link.addEventListener("click", (e) => {
>     e.preventDefault();
>     console.log("clicked");
> })
```




實戰 - 練習寫一個計數器 (減法的值不可以 < 1)
------

```markdown
> HTML
> button id="minus">-</button>
> input type="number" id="counter" value="1">
> button id="plus">+</button>
```

```markdown
> JavaScript
> / 抓中間的顯示器
> onst counter = document.querySelector("#counter")
> 
> / 抓 + 號
> onst plusBtn = document.querySelector("#plus")
> lusBtn.addEventListener("click", () => {
>    counter.value = Number(counter.value) + 1
> )
> 
> 
> / 抓 - 號
> onst minusBtn = document.querySelector("#minus")
> inusBtn.addEventListener("click", () => {
>    const value = Number(counter.value)
>    if (value > 1) {
>        counter.value = value - 1    
>    } 
> )
> 
```





















