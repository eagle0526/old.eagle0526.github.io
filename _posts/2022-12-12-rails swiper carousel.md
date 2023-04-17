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

(1) 輸入下面的指令



rails 6 的指令
```shell
$ yarn add stimulus-carousel
```


rails 7 的指令
```shell
$ bin/importmap pin stimulus-carousel
```

(2) 在controller.js檔案import插件

```md
app/javascript/controllers/index.js

> import { Application } from "stimulus"
> import Carousel from "stimulus-carousel"
> 
> const application = Application.start()
> application.register("carousel", Carousel)
```


(3) 在stylesheets增加兩行指令

```md
> // In your application.js (for example)
> import 'swiper/swiper-bundle.min.css'
> 
>   
> // Or in your application.scss file
> @import "~swiper/swiper-bundle"
```


(4) 在HTML頁面掛上controller、設定屬性

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


(5) 在controller.js中的scss，新增一個swiper_carousel.scss檔案，這邊可以設定輪播圖的樣式
```md

<style>
  .swiper-slide {
    height: 250px;
    display: flex;
    align-items:center;
    justify-content: center;
  }

  .pink {
    background-color: lightpink;
  }

  .green {
    background-color: lightgreen;
  }

  .blue {
    background-color: lightblue;
  }
</style>
```



(6) 增加輪播圖上面的箭頭

```md
index.html.erb

> <div data-controller="carousel" class="swiper-container w-25 my-5"
>     data-carousel-options-value='{
>     "pagination": { "el": ".swiper-pagination", 
>                     "dynamicBullets": "true" },
>     "navigation": { "nextEl": ".swiper-button-next", 
>                     "prevEl": ".swiper-button-prev"}}'>
>   ...
>   <!-- Pagination (... or 1/10 or progress bar) -->
>   <div class="swiper-pagination"></div>
> 
>   <!-- Navigation buttons (< >) -->
>   <div class="swiper-button-prev"></div>
>   <div class="swiper-button-next"></div>
> </div> 
```


參考文章：https://betterprogramming.pub/build-a-carousel-with-ruby-on-rails-and-the-stimulus-components-library-22b1b5e1e682









輸入這一行
```shell
$ rails g stimulus carousel
```


會產生一個檔案 app/javascript/controllers/carousel_controller.js ，並在此檔案，這樣設定
```js
// app/javascript/controllers/carousel_controller.js 

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
















有一網頁有 rails 7 的輪播圖方法，好像很厲害，但是看不太懂
這個網頁 - https://www.remark.social/blog/building-image-carousel-rails-7-stimulus-turbo

```md
<% @houses.each do |house| %>

<div class="relative" data-controller="carousel">
  <div class="absolute top-0 bottom-0 left-0 flex items-center">
    <button data-action="click->carousel#previous" type="button" class="bg-gray-300 rounded-full"><!-- previous icon -->123</button>
  </div>
  
  <div class="absolute top-0 bottom-0 right-0 flex items-center">
    <button data-action="click->carousel#next" type="button" class="bg-gray-300 rounded-full"><!-- next icon -->next</button>
  </div>

  <% house.images.each_with_index do |image, idx| %>    
	<img
	  class="rounded-md"		 
	  width="300px"		
	  src="<%= image.url if image.url %>"
	>
	<div data-carousel-target="image" class="<%= idx > 0 ? "hidden" : nil %>">
      <%=
        turbo_frame_tag "image-#{image.id}",
          class: "absolute top-0 left-0 right-0 bottom-0",
          src: image.url,
          loading: :lazy
      %>	  
	</div>
  <% end %>
</div>

<% end %>

```

