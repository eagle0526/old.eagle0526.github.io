---
title: Rails 圖片輪播教學
author: YeeChen
date: 2022-12-12
category: Rails
layout: post
---


> ---    
> **前情提要：**         
> 本篇教學如何讓圖片使用輪播的方式呈現
>    
> ---    
{: .block-tip}




安裝stimulus-carousel
------

### 輸入下面的指令


安裝 Carousel 套件：您可以使用 yarn 或 npm 安裝任何您喜歡的 Carousel 套件。以下以 swiper 為例，您可以在終端機中執行以下命令：

#### rails 6 的指令
```shell
$ yarn add stimulus-carousel
```


#### rails 7 的指令
```shell
$ bin/importmap pin stimulus-carousel
```



產生controller
------
創建 Stimulus 控制器：在您的 Rails 7 應用中，創建一個 Stimulus 控制器，例如 carousel_controller.js。您可以在 app/javascript/controllers 目錄下創建此文件，並添加以下程式碼：


這個指令，可以產生 `carousel_controller.js` 這個檔案
```shell
$ rails g stimulus carousel
```

接著我們在這個檔案輸入以下程式碼

```js
// carousel_controller.js

import { Controller } from "@hotwired/stimulus";
import { Application } from "@hotwired/stimulus";
import Carousel from "stimulus-carousel";

const application = Application.start();
application.register("carousel", Carousel);

// Connects to data-controller="carousel"
export default class extends Controller {
  connect() {
    super.connect();
    console.log('Do what you want here.');

    // The swiper instance.
    this.swiper;

    // Default options for every carousels.
    this.defaultOptions;
  }
}
```


掛上CDN
------

接著我們來導入CDN，掛載這個CDN，swiper的CSS才會正常顯示

```md
views/layouts/applications.html.erb

<head>
  ... 省略
  掛載此CDN
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/swiper@8/swiper-bundle.min.css"/>
  ... 省略
</head>
```


設定HTML
------

### 1 設定區塊

輸入HTML，我們先用色塊來顯示輪播
```md
index.html.erb

> <!-- Slider main container -->
> <div data-controller="carousel" class="swiper-container">
>   <!-- Additional required wrapper -->
>   <div class="swiper-wrapper">
>     <!-- Slides -->
>     <div class="swiper-slide">Slide 1</div>
>     <div class="swiper-slide">Slide 2</div>
>     <div class="swiper-slide">Slide 3</div>
>   </div>
> </div>
```

照上面輸入的話，會覺得超級怪，因為發現有三個超出畫面的大色塊，是因為我們還沒有把CSS加上去  

### 2 增加色塊的顏色，在div上面掛class
```md
index.html.erb

> <!-- Slider main container -->
> <div data-controller="carousel" class="swiper-container">
>   <!-- Additional required wrapper -->
>   <div class="swiper-wrapper">
>     <!-- Slides -->
>     <div class="swiper-slide green">Slide 1</div>
>     <div class="swiper-slide pink">Slide 2</div>
>     <div class="swiper-slide black">Slide 3</div>
>   </div>
> </div>
```

接著到application.css來寫CSS，我們先增加色塊顏色，還有色塊的高度，讓我們更直觀一點，還有讓色塊的字置中
```md
assets/stylesheets/application.css

.swiper-container {    
   height: 250px;    
}


.black {
    background-color: blue;
}

.pink {
    background-color: pink;
}

.green {
    background-color: green;
}

// 文字置中
.swiper-slide {
  background-position: center;
  background-size: cover;
  
  display: flex;
  align-items:center;
  justify-content: center;
}
```


### 3 增加箭頭、導覽圈圈

使用data-carousel-options-value，可以增加輪播圖的特色，因此我們在這邊新增pagination、navigation
```md
> <section class="good">   
>   <!-- Slider main container -->
>   <div class="swiper-container slide" data-controller="carousel" 
>                                         data-carousel-options-value='{
>                                           "pagination": { "el": ".swiper-pagination", 
>                                                           "dynamicBullets": "true" },
>                                           "navigation": { "nextEl": ".swiper-button-next", 
>                                                           "prevEl": ".swiper-button-prev"}
>                                           }'>
>   
>     <!-- Additional required wrapper -->
>     <div class="swiper-wrapper">
>       <!-- Slides -->
>       <div class="swiper-slide green">Slide 1</div>
>       <div class="swiper-slide pink">Slide 2</div>
>       <div class="swiper-slide black">Slide 3</div>
>     </div>
>   
>       <!-- Add Pagination -->
>     <div >
>       <div class="swiper-pagination"></div>
>   
>       <!-- Add Navigation -->
>       <div class="swiper-button-next"></div>
>       <div class="swiper-button-prev"></div>
>     </div>
>   
>   </div>
> </section>
```

### 4 讓圖片使用fade模式

不過現在看還是很奇怪對不對，因為圖片還是三張橫排，所以我們現在增加一個特效，讓圖片可以重疊，並且當我按袖邊箭頭的時候，會切換到下一張
```md
> <section class="good">   
>   <!-- Slider main container -->
>   <div class="swiper-container slide" data-controller="carousel" 
>                                           data-carousel-options-value='{
>                                             "pagination": { "el": ".swiper-pagination", 
>                                                             "dynamicBullets": "true" },
>                                             "navigation": { "nextEl": ".swiper-button-next", 
>                                                             "prevEl": ".swiper-button-prev"},

>                                             // 這一行
>                                             "effect": "fade"
>                                             }'>

>   
>     <!-- Additional required wrapper -->
>     <div class="swiper-wrapper">
>       <!-- Slides -->
>       <div class="swiper-slide green">Slide 1</div>
>       <div class="swiper-slide pink">Slide 2</div>
>       <div class="swiper-slide black">Slide 3</div>
>     </div>
>   
>       <!-- Add Pagination -->
>     <div >
>       <div class="swiper-pagination"></div>
>   
>       <!-- Add Navigation -->
>       <div class="swiper-button-next"></div>
>       <div class="swiper-button-prev"></div>
>     </div>
>   
>   </div>
> </section>
```



### 5 讓箭頭和導覽圈圈待在圖片裡面

如果今天你不想讓圖片這麼大，想縮小輪播圖的寬度，卻發現當你修改最外層swiper-container這個CSS寬度的時候，會發現箭頭和導覽列沒有被縮小到，這是因為他們兩個目前是絕對定位的情況  
所以只要幫swiper-container加上相對定位，就可以把他們限制在輪播圖裡面
```md
assets/stylesheets/application.css

> .swiper-container {  
>    height: 250px;
>    position: relative;
> }
```







最終程式碼
------

```js
// carousel_controller.js

import { Controller } from "@hotwired/stimulus";
import { Application } from "@hotwired/stimulus";
import Carousel from "stimulus-carousel";

const application = Application.start();
application.register("carousel", Carousel);

// Connects to data-controller="carousel"
export default class extends Controller {
  connect() {
    super.connect();
    console.log('Do what you want here.');

    // The swiper instance.
    this.swiper;

    // Default options for every carousels.
    this.defaultOptions;
  }
}
```

```md
assets/stylesheets/application.css

> .swiper-container {
>    /* width: 300px; */
>    height: 500px;
>    position: relative;
> }
> 
> 
> .black {
>     background-color: blue;
> }
> 
> .pink {
>     background-color: pink;
> }
> 
> .green {
>     background-color: green;
> }
> 
> 
>   
> .swiper-slide {
>   background-position: center;
>   background-size: cover;
> 
>   /* height: 250px; */
>   display: flex;
>   align-items:center;
>   justify-content: center;
> }
>   
> 
> .swiper-pagination {
>     background-color: aquamarine;
> }
> 
> 
> 
> .good {
>     padding: 0px 200px;
>     
> }
```


```md
index.html.erb

> <section class="good">   
>   <!-- Slider main container -->
>   <div class="swiper-container slide" data-controller="carousel" 
>                                           data-carousel-options-value='{
>                                             "pagination": { "el": ".swiper-pagination", 
>                                                             "dynamicBullets": "true" },
>                                             "navigation": { "nextEl": ".swiper-button-next", 
>                                                             "prevEl": ".swiper-button-prev"},
>                                             "effect": "fade"
>                                             }'>
>   
>     <!-- Additional required wrapper -->
>     <div class="swiper-wrapper">
>       <!-- Slides -->
>       <div class="swiper-slide green">Slide 1</div>
>       <div class="swiper-slide pink">Slide 2</div>
>       <div class="swiper-slide black">Slide 3</div>
>     </div>
>   
>       <!-- Add Pagination -->
>     <div >
>       <div class="swiper-pagination"></div>
>   
>       <!-- Add Navigation -->
>       <div class="swiper-button-next"></div>
>       <div class="swiper-button-prev"></div>
>     </div>
>   
>   </div>
> </section>
```