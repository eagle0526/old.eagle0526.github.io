---
title: Rails Polymorphic實際案例 - 留言、房子都會被使用者點讚
author: YeeChen
date: 2022-12-10
category: Rails
layout: post
---


> ---    
> **前情提要：**         
> 一間房子可以被使用者點讚/倒讚  
> 一則留言可以被使用者點讚/倒讚  
> 
> ---    
{: .block-tip}

















### 最終程式碼



#### 控制房子喜歡/不喜歡按鈕的js頁面
```md
house_like_controller.js

> import { Controller } from "@hotwired/stimulus"
> import { library, dom } from '@fortawesome/fontawesome-svg-core'
> import { faHeartCrack } from '@fortawesome/free-solid-svg-icons' 
> import { faHeart } from '@fortawesome/free-regular-svg-icons'
> 
> export default class extends Controller {
> 
>   static targets = [ 'heart', "heartCrack", "houseLikeCount" ]
> 
>   initialize(){    
>     library.add(faHeart, faHeartCrack)
>   }
>   connect() {
>     dom.watch()    
> 
>     // 一進來就先判斷，LikeState中的state到底是空的還是false還是true
>     const likeState = this.element.dataset.likeState
> 
>     if (likeState === 'true') {      
>       this.heartBlue()
>     } else if (likeState === 'false') {      
>       this.heartCrackBlue()
>     }
> 
>   }
> 

>   // 點擊愛心的動作    
>   heart() {    
>     const houseID = this.element.dataset.id
>     const token = document.querySelector("meta[name='csrf-token']").content   
> 
>     // 這個是新增like的路徑 - /houses/:id/like
>     fetch(`/houses/${houseID}/like`, {
>       method: "PATCH",
>       headers: {
>         "X-CSRF-Token": token
>       },
>       body: JSON.stringify(params),
>     })
>     .then((resp) => {
>       return resp.json()
>     })
>     .then(({status, houseLikeCount, houseDislikeCount}) => {      
> 
>       if (status === "liked house") {
>         this.heartBlue()
>       } else if ( status === 'delete house like_state' ) {
>         this.heartWhite()
>       } else {
>         this.heartBlue()
>         this.heartCrackWhite()
>       }
> 
>     
>     // 這邊把後端傳來的實際數量，再用dispatch傳到顯示數量的controller
>     const increaseCount = new CustomEvent("increase", {
>       detail: {houseLikeCount: houseLikeCount, houseDislikeCount: houseDislikeCount}
>     }) 
>     window.dispatchEvent(increaseCount)
> 
>     })
>     .catch((err) => {
>       console.log(err);
>     })
>     
>   }
> 
>   // 點擊破碎愛心的動作
>   heartCrack() {
> 
>     const houseID = this.element.dataset.id
>     const token = document.querySelector("meta[name='csrf-token']").content
> 
>     fetch(`/houses/${houseID}/dislike`, {
>       method: "PATCH",
>       headers: {
>         "X-CSRF-Token": token
>       }
>     })
>     .then((resp) => {
>       return resp.json()
>     })
>     .then(({status, houseLikeCount, houseDislikeCount}) => {      
>       if (status === "disliked houses") {
>         this.heartCrackBlue()
>       } else if (status === "delete house like_state")  {
>         this.heartCrackWhite()
>       } else {
>         this.heartCrackBlue()
>         this.heartWhite()
>       }
> 
>       // 這邊把後端傳來的實際數量，再用dispatch傳到顯示數量的controller
>       const decreaseCount = new CustomEvent("decrease", {
>         detail: {houseLikeCount: houseLikeCount, houseDislikeCount: houseDislikeCount}
>       }) 
>       window.dispatchEvent(decreaseCount)
>     })
>     .catch((err) => {
>       console.log(err);
>     }) 
>   }
> 
> 
>   // 把愛心底色加上藍色
>   heartBlue() {
>     this.heartTarget.classList.add("bg-blue-100")
>   }
> 
>   // 把愛心底色加上白色
>   heartWhite() {
>     this.heartTarget.classList.remove("bg-blue-100")
>   }
> 
>   // 把破碎愛心底色加上藍色
>   heartCrackBlue() {
>     this.heartCrackTarget.classList.add("bg-blue-100")
>   }
> 
>   // 把破碎愛心底色加上白色
>   heartCrackWhite() {
>     this.heartCrackTarget.classList.remove("bg-blue-100")
>   }
> 
> }
```






