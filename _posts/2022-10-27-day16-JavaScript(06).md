---
title: ASTRO Camp Day16 - JavaScript(06)
author: YeeChen
date: 2022-10-27
category: JavaScript
layout: post
---


事件流
------

JS的事件留有三階段

如果今天有兩層結構，會先往下穿過外層到內層
再從內層到外層
第一階段 -> 捕獲階段 (capturing) 
第二階段 -> targeting 
第三階段 -> 冒泡階段 (bubbing) 



事件監聽器的第三個參數，預設值是false


(第三個參數，如果是Ture，就會是capturing階段)
(第三個參數，如果是false，就會是bubbing階段)



這個東西做遊戲會用到，像是卡牌遊戲



如果今天Ａ內層有Ｂ，但是我想要按B不出現A，要怎麼做

事件停止傳播
Event.stopPropagation()

直接在B下 e.stopPropagation()
這樣事件流就會停在B，就會只印出B



今天想點擊內層B層，但只出現A要怎麼做
穿不過A的

A.addEventListener("click", (e) => {
    e.stopPropagation()                 -> 停在A
    console.log("A");
}, true)                                -> capture階段
B.addEventListener("click", (e) => {
    console.log("B");
})



target階段

如果今天對監聽器下
e.target

他會印出target前一層的traget
如果今天事件流下在capture
target就會抓最內層的，if A 包住 B，就會印出B

如果今天事件流下在bubbing
target就會抓最內層的，if A 包住 B，就會印出B




currentTarget // 註冊事件的那傢伙，永遠不會因為事件流的而改變






什麼是範圍Scope
------

Scope Chain - 內部找不到變數，就往外找


Lecical Scope - Scope跟他寫在哪裡有關
下面就是一個 Lecical Scope 的狀況
最後最呼叫出hey()，並印出2

let a = 1

function hello() {
    let a = 2
    console.log(a)
}

function hey() {
    console.log(a)
}


hello() -> 2








'use strict'
------

fuction hi() {
    'use stict'         -> 加上這個，就會對此函數有嚴格的標準
    a = 2                  如果沒有宣告，就不會自動在window生成變數
    console.log(2)
}

hi()









// 每秒增加一
for(let i = 3; i < 0; i++) {
    setTimeOut(() => {
        console.log("A")
    }, 1000 * (i+1))
}






currentSec = sec

let state = "stop"
多做一個判斷
如果狀態是runngning



多宣告一個變數 - 狀態變數
假設現在是開始，就把狀態改成stop
並





***




物件導向
------

物件導向的目的，用比較容易理解的方式，來整理你的程式碼，並把那些fc放到對的地方

下面是一個hero物件
```markdown
> const hero = {
>     name: "kk",
>     power: 100,
>     attack: function() {
>         console.log("attack!!!)
>     }
>  }

> 呼叫hero的attack fc
> hero.attack();                    # attack!
```


**但是假如今天要是在做遊戲，要做一個小兵模組，總不會每一個小兵都像上面那樣一個一個物件生成，這樣太慢**


因此我們來建立一個英雄模組，並且這個模組要傳兩個參數進去
(客製化英雄的名字、力量)
```markdown
> function heroCreator(name, power) {
>     const hero = {
>         name: name,                  -> 把函式的name傳給物件
>         power: power,                          power
>         attack: function() {
>             console.log("attack!!!)
>         }
>     }
>     return hero;
> }

> 這樣就可以直接創造出一個英雄
> (這樣寫，以後想要生成一個英雄，只要heroCreator(引數, 引數)，這樣這就)
> const h1 = heroCreator("kk", 100)
> h1.attack();
```


> --  
> 但是像上面這樣寫會遇到一個狀況，假設現在有h1, h2, h3，都用heroCreator生成，這樣會三個新物件，都會有同樣的attack函式，因為記憶體存量的關係，如果我們把這個fc抽出來，可以大大的減少記憶體消耗  
>  
> ex.以遊戲子彈為例，每一個子彈都是一個物件，如果每一個子彈都獨立出一個fc，這樣消耗太多記憶體
>     
> --  
{: .block-tip}



Object_create(proto) - 參數可加可不加
------


下面的創造物件的寫法跟上面的寫法的結果一樣

```md
> function heroCreator(name, power) {
> 
>     const hero = Object.create(null)     -> 先做一個空的物件
>     hero.name = name;                    -> 屬性一個一個加上去
>     hero.power = power;                  -> 屬性一個一個加上去
>     hero.attack = function() {           -> 屬性一個一個加上去  
>         console.log("attack!")
>     }
> 
>  }
>     return hero;
> }

> const h1 = heroCreator("kk", 100)
> console.log(h1)                          -> 這個物件印出來，也會有name, power, fc
```


> --  
> Object_create神奇的地方就在於，如果今天這邊  
> Object.create(null) -> 這個null位置的參數，他是一個原型(prototype)，他會根據原型去打造一個東西出來  
> --  
{: .block-tip}





原型打造 prototype 
------

- 原型打造的意思是，根據某個東西，打造出相似的東西出來
- 如果今天Object.create(null)，是null，代表我沒有要參考任何原型


今天定義一個物件，裡面有兩個fc
const actions =  {
    attack: function() {
        console.log("attack!!!!!!")
    },
    sleep: function() {
        console.log("zzzzzzzzzZZZ")
    }
}


然後我在剛剛那個heroCreator的Object.create把 actions 傳進去  
這代表的意思是，我要用 actions物件 當作我的原型，去打造一個新的原型出來  
```md
> function heroCreator(name, power) {
> 
>     const hero = Object.create(actions)      -> 繼承actions物件的功能      
>     hero.name = name;
>     hero.power = power;
>     hero.attack = function() {
>         console.log("attack!")
>     }
> 
>  }
>     return hero;
> }
> 
> 這樣我們會印出什麼，會發現h1印出來多了一個 Prototype 的東西，而fc就塞在那裡面
> const h1 = heroCreator("kk", 100)
> console.log(h1)                          -> {name: "kk", power: 100, [[Prototype]]-> 函式在這裡面}

> 因為函式在Prototype的關係，所以  
> h1.attack()  
> h1.sleep()  
> 這樣寫兩個一樣都可以動，這個新物件有繼承actions的函式 
```

__proto__
------

> --  
> 當我要找某個物件的屬性時，JS會試著先找物件本身，如果物件本身沒有跟屬性，會循著另一個管道去找該屬性   
> 這個管道就是__proto__  
>    
> 所有的物件都有很特別的屬性，叫做 **__proto__**  
> **__proto__**這個特性是，他要找東西的時候，會一直沿著物件去尋找，直到找不到東西為止  
> --  
{: .block-tip}

### 原型鏈 - hero.__proto__.__proto__

原型鏈的好是什麼，就是可以把共通的fc放到上層，要用的時候，再去上層拿取就好，可以大大減輕物件的大小

```md
> 假設我今天創造一個新的物件hero
> 然後再我要找hero物件的某個屬性
> ex. ability屬性
> 
> 這樣的話我們可以在console打上
> hero.ability
> 這樣的話就代表我想要找h1物件的屬性
> 
> 那實際上程式是怎麼去找這個ability的
> 是這樣 
> hero.__proto__
> 這個會去找hero前一層還有沒有屬性
> 如果往前一層還沒找到，但是沒有印出錯誤訊息
> 就再往前一層找
> hero.__proto__.__proto__
> 直到印出null為止
> 
> 這一直_proto_找尋屬性的行為，就是叫做原型鏈
```

> --  
> 這邊我一直提到上層，其實不太精確，因為對於原型鏈來說，其實是下一個鏈結 - 下一個鏈結   
> --  
{: .block-warning}



```md
> 所以如果我今天這樣打，會印出true，因為h1往上一層找，可以找到actions物件
> code 在 原型打造 那邊

> h1.__proto__ === actions    # true
```




原型鏈實際範例
------

你現在寫一個 
```md
> const list = [1,2,3,4]
```

我們想對這個list寫一個map方法，那這個map放在哪裡呢?就放在陣列的上一層
```md
> list.__proto__ -> 可以找到 map的寫法
```





new 新物件
------

另外一種方法，如果今天有在前方寫給new，會直接在函式裡面給一個{}空物件  
  
這個new會幫我們做幾件事情
- 產生一個空的物件
- 會有一個 this 指向空物件
- 自動 return 物件
- 


```md
> fuction heroCreator (name, power) {
>     // this -> {}       -> this會指向new出來的空物件
>     this.name = name;
>     this.power = power
>     // return this      -> 這個this會順便幫你回傳值，不用自己寫
> }
> const h1 = **new** heroCreator("kk", 100)   -> 這邊加一個new

> 這樣我們直接印就有結果了
> console.log(h1)                # heroCreator {name: "kk", power: 100}
```

> --  
> 如果今天上面那一串，在創造新物件的時候沒有寫 new 的話，會印出 undefined  
> --  
{: .block-tip}




new 傳進 actions 的方法
------

不過目前new這個方式，會有一個問題，沒有繼承actions的功能  
如果 new 寫法，想要把 actions 傳進去，要怎麼寫呢  

```md
> fuction heroCreator (name, power) {       
>     // {}.__proto__ = heroCreator.prototype  -> new 物件的時候還會做這一件事
>     // this -> {}
>
>     this.name = name;
>     this.power = power
>     // return this      -> 這個this會順便幫你回傳值，不用自己寫
> }
> const h1 = **new** heroCreator("kk", 100)   -> 這邊加一個new


```md
> #### 下面這一句的意思就是，把一個空物件指向一個空物件
> {}.__proto__ = heroCreator.prototype 
> 
> {}.__proto__ =  {} 空物件
> heroCreator.prototype = {} 空物件
> 
> ex. 當有人有去找__proto__的時候，請去找heroCreator這個做這過人的prototype
```



> --  
> 所有物件都有 __proto__ 屬性  
> 所有 fn 都有 prototype 屬性、__proto__屬性  => 所有 fc 的 prototype 都是空物件
> (只有fn同時都有兩個屬性)  
> --  
{: .block-tip}




如果我今天這樣寫，可以幫新創的heroCreator物件新增功能
```md
> heroCreator.prototype.aaa = "123"
> h1.aaa                      # 123
```


### 回到原點 - 剛剛說要用 new 繼承 某個物件的函式

```md
> fuction heroCreator (name, power) {       
>
>     this.name = name;
>     this.power = power
>     // return this      
> }

> heroCreator.prototype = actions               -> 直接在這邊加上想要繼承的物件，就可以成功
> const h1 = new heroCreator("kk", 100)   

> h1.attack()                   # attack!!!     -> 新物件可以印出actions的函式




### mdn上Array.prototype.map()的由來
```md
> const a = new Array()             -> 用 new 創造一個變數a陣列
> a.__proto__ === Array.prototype   # true
> a.map === Array.prototype         # true
```



### 實際更改Array功能
```md
> 像下面這樣寫，就可以幫助所有陣列增加.hello功能
> Array.prototype.hello = function() {
>     console.log("hi")
> }
> 
> 但實際上不會特別去寫
```


***


Class 比較常在用的寫法
------

```md
> Class heroCreator {
>     constructor(name, power) {    -> constructor 固定寫法
>         this.name = name;
>         this.power = power
>     }
> 
>     attack() {
>         console.log("attack!")
>     }
> }
> 
> const h1 = new heroCreator("kk", 100)  
> console.log(h1)                           -> 結果跟剛剛上面一樣
```


Ps.如果今天用Class寫法，創新物件的時候沒有給new，系統會直接報錯 -> TypeError





繼承
------

物件導向真正的意義，把共通的行為放到最裡面層，想要用的時候在叫出來用，比較好管理

```md
> class Animal {                                -> 設定一個上層動物類型
>     constructor(name, power) {                -> 這個constructor是固定寫法，類似ruby的initialize
>         this.name = name;
>         this.power = power;
>     }
> }
> 
> 
> class HeroCreator **extends** Animals {       -> 類別英雄繼承animals的類別
>     attack() {
>         console.log("attack!!!!!!")
>     }
> }
> 
> 
> cosnt h1 = new HeroCreator("kk", 100)
> 
> console.log(h1)         # HeroCreator {name: "kk", power: 100} -> 一樣有相同的屬性
> 
> h1.__proto__            # Animal {constructor} -> proto會指向上一層
```




### 面試會考的題目

```md
> 1. ll objects have prototype -> false 
> (是所有 fc 都有prototype)

> **
> 2. 箭頭函式沒有prototype
> **

> 3. 使用new實體時，在類別裡面return 會發生什麼事
> 
> function Cat(name) {
>     this.name = name
>     return 123             -> 如果今天刻意給實體 return  (正常人不會在這邊return)
> }
> 
> const c = new Cat("cc")    -> 實際上會忽略上面傳下來的123，一樣是傳Cat下來
> console.log(c)
```


***



分號到底要不要加
------


如果要換行，可以加一個小括號

return (
    1+2
)


ASI auto semicolon Insertion

console.log(123)
[1,2,3].map((x) => {})   -> 這樣兩行都不加分號的話，會無法執行

是因為ASI其中一個規則，如果下一行是一個中括號[]的話，前面一行code的尾端他就不為自動幫你加分號




***


this - 一種代名詞
------

### 1. 誰呼叫，誰就是this

const hero = {
    hi: function() {
        console.log(this)   -> 這個this就是hero
    }
}
hero.hi()




另一種狀況
fuction hi() {
    function hey() {
        const hero = {
            name: "kk"
            action: function () {
                console.log(this.name)   -> 這個this 是 hero
            }
        }
        
    }
    hero.action()
}

hi()

### 2. 沒人呼叫

fuction hi() {
    console.log(this)       -> 這個this會變成全域物件
}

hi()



另一種狀況
fuction hi() {
    function hey() {
        console.log(this)       -> 這個this也是全域物件
    }
    hey()                        
}

hi()






### 3. 箭頭函式沒有自己的this -> 16:38 的影片，記得把整段code打下來試試

const btn = document.querySelector("#btn")

btn.addEventListener("click", ()=>{           
    console.log(this)                   -> 這個this因為箭頭函式，所以全域物件
})




### 4. 是否有使用 new

function hi(age) {
    
    this.age = age  -> this會直接在全域產生一個 age 變數
}


const h = hi(18)   -> 如果今天沒有使用 new
console.log(h)
console.log(age)   -> 這裡會直接可以印出 18 

**不過這很可怕，要記得加上new








### 5. 是否有使用 apply, call, bind

先給一個物件
```md
> const hero = {
>     name: "kk"
>     action: function() {
>         console.log(this.name);    -> 這會印出 kk
>     }
> }
> #### 呼叫物件中的函式
> hero.action()
```


用.call來呼叫
```md
> const hero = {
>     name: "kk"
>     action: function() {
>         console.log(this.name);    -> 這個this會變成 cc 
>     }
> }
> 
> const cc = { name: "cc" }
> hero.action.call(cc)   -> 會印出 "cc"
```


.call呼叫方法可以帶參數，回傳進去呼叫的物件裡面
```md
> const hero = {
>     name: "kk"
>     action: function(n, m) {
>         console.log(this.name, n, m);    ->  印出 cc, 1, 2
>     }
> }
> 
> const cc = {name: "cc"}
> hero.action.call(cc, 1, 2)   -> 這1, 2 會傳上去function裡面
```

> --  
> **call 跟 apply 的差異**  
> call後面參數是接多個數字  
> apply後面是接陣列  
> --
{: .block-tip}



### call物件實際案例

```md
> 先生成一個戰士物件
>
> const hero = {
>     hp: 100,
>     mp: 20,
>     attack: function() {
>         console.log("attack!!!!!")
>     }
> }
>
> 再生成一個法師物件，多一個補血技能，用call方法可以幫戰士補血
> const mage = {
>     hp: 70,
>     mp: 80,
>     attack: function() {
>         console.log("attack!!!!!")
>     }
>     heal: function() {
>         this.hp += 30  -> this 會依照下面的方法更改對象(call方法)
>     }
> }
> 
> mage.heal.call(hero)   -> 這樣寫可以幫英雄補血，因為call可以改變傳進來技能的指向
```




