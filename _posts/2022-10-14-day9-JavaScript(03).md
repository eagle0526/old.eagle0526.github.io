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
> 
> 
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
>     result,push(item*2)            # [2,4,6,8,10]
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



何謂高階函數 higher-order function
 - 可以把 fn 當作參數傳入另一個 fn
 - 可以回傳 fn










