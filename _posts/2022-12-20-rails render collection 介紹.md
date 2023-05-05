---
title: Rails render collection
author: YeeChen
date: 2022-12-20
category: Rails
layout: post
---


> ---    
> **前情提要：**         
> 在迴圈內渲染其他頁面時候，rails有推薦使用collection這個方法，使用此方法就可以讓效能變更好，因此我們來看詳細的數據，確認使否有讓效能變好
>    
> ---    
{: .block-tip}



基本設定
------

### controller

以下是我們的controller設定，現在只有專注在 `show action` 就好，其他都不必在意
```rb
class PostsController < ApplicationController
  before_action :authenticate_user!
  before_action :find_post, only: [:show, :edit, :update, :destroy]
    
  # ...省略

  def show      
    @comment = Comment.new

    # 下面這一行是我們要用到的
    @comments = @post.comments.where(parent_id: nil).order(id: :desc)
  end
  
  private
  def find_post
    @post = Post.find_by(id: params[:id])        
  end
end
```

PS. 順便說一下為啥後面要有where那一段，因為我們有做子留言系統，一個留言今天如果有人要對此留言做回覆，該留言就會產生一個parent_id，所以如果今天留言沒有parent_id，就代表該留言是父留言


### view

下面這樣留言方式，就可以渲染出這個頁面 `comments/comment` 的東西，因此我們要再去該頁面做設定
```html
<!-- views/posts/show.html.erb -->

<h4>我是大家的留言</h4>

<ul class="ul">
    
  <% @comments.each do |comment| %>
    <%= render "comments/comment", comment: comment %>
  <% end %>
  
</ul>
```

照下面的設定，我們想要把留言的內容寫出來，這樣寫後，就可以把所有留言都顯示出來了
```html
<!-- views/comments/_comment.html.erb -->

<p><%= comment.content %></p>
```

### render collection 改寫


但是當我們在迴圈裡面，渲染另外一個頁面的時候，效能不太好，因此rails也建議使用一個方法，也就是下面這樣：
```html
<!-- views/posts/show.html.erb -->

<h4>我是大家的留言</h4>

<ul class="ul">
  
  <!-- 這個是原始版本，partial 就是我們想要渲染的頁面，collection就是我們想要跑的迴圈，as是我們想要傳進去的參數 -->
  <%#= render partial: "comments/comment", collection: @comments, as: :comment %>

  <!-- 如果今天格式都像上面那樣符合格式，我們可以直接像這樣縮寫 -->
  <%= render @comments %>
  
</ul>
```

不過這個效能真的有比較好嗎？我們來把所有終端機的數據全部都列出來看


### 沒用collection的寫法

先寫出HTML
```html
<h4>我是大家的留言</h4>

<ul class="ul">
    
  <% @comments.each do |comment| %>
    <%= render "comments/comment", comment: comment %>
  <% end %>
  
</ul>
```



完整數據，但是這邊數據太雜了，我把重要的部分欻出來
```md
>Processing by PostsController#show as HTML
>  Parameters: {"id"=>"12"}
>  User Load (0.1ms)  SELECT "users".* FROM "users" WHERE "users"."id" = ? ORDER BY "users"."id" ASC LIMIT ?  [["id", 6], ["LIMIT", 1]]
>  ↳ app/controllers/application_controller.rb:4:in `authenticate_user!'
>  Post Load (0.4ms)  SELECT "posts".* FROM "posts" WHERE "posts"."id" = ? LIMIT ?  [["id", 12], ["LIMIT", 1]]
>  ↳ app/controllers/posts_controller.rb:59:in `find_post'
>  Rendering layout layouts/application.html.erb
>  Rendering posts/show.html.erb within layouts/application
>  Rendered comments/_form.html.erb (Duration: 1.2ms | Allocations: 605)
>  Comment Load (0.1ms)  SELECT "comments".* FROM "comments" WHERE "comments"."deleted_at" IS NULL AND "comments"."post_id" = ? AND "comments"."parent_id" IS NULL ORDER BY "comments"."id" DESC  [["post_id", 12]]
>  ↳ app/views/posts/show.html.erb:61
>  Rendered comments/_form.html.erb (Duration: 0.5ms | Allocations: 603)
>  Comment Load (0.1ms)  SELECT "comments".* FROM "comments" WHERE "comments"."deleted_at" IS NULL AND "comments"."parent_id" = ?  [["parent_id", 75]]
>  ↳ app/views/comments/_comment.html.erb:17
>  Rendered comments/_comment.html.erb (Duration: 2.4ms | Allocations: 1808)
>  Rendered comments/_form.html.erb (Duration: 0.4ms | Allocations: 603)
>  Comment Load (0.0ms)  SELECT "comments".* FROM "comments" WHERE "comments"."deleted_at" IS NULL AND "comments"."parent_id" = ?  [["parent_id", 74]]
>  ↳ app/views/comments/_comment.html.erb:17
>  Rendered comments/_comment.html.erb (Duration: 2.1ms | Allocations: 1808)
>  Rendered comments/_form.html.erb (Duration: 0.4ms | Allocations: 603)
>  Comment Load (0.0ms)  SELECT "comments".* FROM "comments" WHERE "comments"."deleted_at" IS NULL AND "comments"."parent_id" = ?  [["parent_id", 73]]
>  ↳ app/views/comments/_comment.html.erb:17
>  Rendered comments/_comment.html.erb (Duration: 2.0ms | Allocations: 1808)
>  Rendered posts/show.html.erb within layouts/application (Duration: 10.2ms | Allocations: 7670)
>[Webpacker] Everything's up-to-date. Nothing to do
>  Rendered shared/_navbar.html.erb (Duration: 0.2ms | Allocations: 296)
>  Rendered shared/_flash.html.erb (Duration: 0.1ms | Allocations: 57)
>  Rendered layout layouts/application.html.erb (Duration: 20.7ms | Allocations: 14779)
>Completed 200 OK in 27ms (Views: 20.9ms | ActiveRecord: 0.8ms | Allocations: 16951)
```

重點擷取：該篇文章目前有三則留言，因此這邊有印出三次留言的數據
```md
>  Comment Load (0.1ms)  SELECT "comments".* FROM "comments" WHERE "comments"."deleted_at" IS NULL AND "comments"."parent_id" = ?  [["parent_id", 75]]
>  ↳ app/views/comments/_comment.html.erb:17
>  Rendered comments/_comment.html.erb (Duration: 2.4ms | Allocations: 1808)
>  Rendered comments/_form.html.erb (Duration: 0.4ms | Allocations: 603)
>  Comment Load (0.0ms)  SELECT "comments".* FROM "comments" WHERE "comments"."deleted_at" IS NULL AND "comments"."parent_id" = ?  [["parent_id", 74]]
>  ↳ app/views/comments/_comment.html.erb:17
>  Rendered comments/_comment.html.erb (Duration: 2.1ms | Allocations: 1808)
>  Rendered comments/_form.html.erb (Duration: 0.4ms | Allocations: 603)
>  Comment Load (0.0ms)  SELECT "comments".* FROM "comments" WHERE "comments"."deleted_at" IS NULL AND "comments"."parent_id" = ?  [["parent_id", 73]]
>  ↳ app/views/comments/_comment.html.erb:17
>  Rendered comments/_comment.html.erb (Duration: 2.0ms | Allocations: 1808)
>  Rendered posts/show.html.erb within layouts/application (Duration: 10.2ms | Allocations: 7670)

<!-- 最終時間 -->
> Completed 200 OK in 27ms (Views: 20.9ms | ActiveRecord: 0.8ms | Allocations: 16951)
```

可以看到，大約渲染出一個留言，要花 `1808`，最終渲染該頁面的時間大約是 `16951`。

Ps. 那個_form是我在_form頁面，有放一個text_field表單，也就是使用者可以對留言做回覆，不過這邊可以先忽略



### 用collection的寫法

```html
<h4>我是大家的留言</h4>

<ul class="ul">
  
  <%= render @comments %>

</ul>

```


完整數據，但是這邊數據太雜了，我把重要的部分欻出來
```md
> Started GET "/posts/12" for ::1 at 2023-05-06 02:39:05 +0800
> Processing by PostsController#show as HTML
>   Parameters: {"id"=>"12"}
>    (0.1ms)  SELECT sqlite_version(*)
>   ↳ app/controllers/application_controller.rb:4:in `authenticate_user!'
>   User Load (0.5ms)  SELECT "users".* FROM "users" WHERE "users"."id" = ? ORDER BY "users"."id" ASC LIMIT ?  [["id", 6], ["LIMIT", 1]]
>   ↳ app/controllers/application_controller.rb:4:in `authenticate_user!'
>   Post Load (1.5ms)  SELECT "posts".* FROM "posts" WHERE "posts"."id" = ? LIMIT ?  [["id", 12], ["LIMIT", 1]]
>   ↳ app/controllers/posts_controller.rb:59:in `find_post'
>   Rendering layout layouts/application.html.erb
>   Rendering posts/show.html.erb within layouts/application
>   Rendered comments/_form.html.erb (Duration: 2.9ms | Allocations: 929)
>   Comment Load (1.5ms)  SELECT "comments".* FROM "comments" WHERE "comments"."deleted_at" IS NULL AND "comments"."post_id" = ? AND "comments"."parent_id" IS NULL ORDER BY "comments"."id" DESC  [["post_id", 12]]
>   ↳ app/views/posts/show.html.erb:59
>   Rendered comments/_form.html.erb (Duration: 0.7ms | Allocations: 603)
>   Comment Load (0.2ms)  SELECT "comments".* FROM "comments" WHERE "comments"."deleted_at" IS NULL AND "comments"."parent_id" = ?  [["parent_id", 75]]
>   ↳ app/views/comments/_comment.html.erb:17
>   Rendered comments/_form.html.erb (Duration: 0.6ms | Allocations: 603)
>   Comment Load (0.1ms)  SELECT "comments".* FROM "comments" WHERE "comments"."deleted_at" IS NULL AND "comments"."parent_id" = ?  [["parent_id", 74]]
>   ↳ app/views/comments/_comment.html.erb:17
>   Rendered comments/_form.html.erb (Duration: 0.6ms | Allocations: 603)
>   Comment Load (0.1ms)  SELECT "comments".* FROM "comments" WHERE "comments"."deleted_at" IS NULL AND "comments"."parent_id" = ?  [["parent_id", 73]]
>   ↳ app/views/comments/_comment.html.erb:17
>   Rendered collection of comments/_comment.html.erb [3 times] (Duration: 10.4ms | Allocations: 5823)
>   Rendered posts/show.html.erb within layouts/application (Duration: 29.8ms | Allocations: 9279)
> [Webpacker] Everything's up-to-date. Nothing to do
>   Rendered shared/_navbar.html.erb (Duration: 1.2ms | Allocations: 792)
>   Rendered shared/_flash.html.erb (Duration: 0.6ms | Allocations: 222)
>   Rendered layout layouts/application.html.erb (Duration: 52.0ms | Allocations: 17714)
> Completed 200 OK in 88ms (Views: 51.9ms | ActiveRecord: 4.5ms | Allocations: 21571)
```


重點擷取：該篇文章目前有三則留言，跟前面沒用collection相比，這邊多了一個很有趣的東西 `[3 times]`
```md
>   Comment Load (1.5ms)  SELECT "comments".* FROM "comments" WHERE "comments"."deleted_at" IS NULL AND "comments"."post_id" = ? AND "comments"."parent_id" IS NULL ORDER BY "comments"."id" DESC  [["post_id", 12]]
>   ↳ app/views/posts/show.html.erb:59
>   Rendered comments/_form.html.erb (Duration: 0.7ms | Allocations: 603)
>   Comment Load (0.2ms)  SELECT "comments".* FROM "comments" WHERE "comments"."deleted_at" IS NULL AND "comments"."parent_id" = ?  [["parent_id", 75]]
>   ↳ app/views/comments/_comment.html.erb:17
>   Rendered comments/_form.html.erb (Duration: 0.6ms | Allocations: 603)
>   Comment Load (0.1ms)  SELECT "comments".* FROM "comments" WHERE "comments"."deleted_at" IS NULL AND "comments"."parent_id" = ?  [["parent_id", 74]]
>   ↳ app/views/comments/_comment.html.erb:17
>   Rendered comments/_form.html.erb (Duration: 0.6ms | Allocations: 603)
>   Comment Load (0.1ms)  SELECT "comments".* FROM "comments" WHERE "comments"."deleted_at" IS NULL AND "comments"."parent_id" = ?  [["parent_id", 73]]
>   ↳ app/views/comments/_comment.html.erb:17
>   Rendered collection of comments/_comment.html.erb [3 times] (Duration: 10.4ms | Allocations: 5823)
>   Rendered posts/show.html.erb within layouts/application (Duration: 29.8ms | Allocations: 9279)

<!-- 最終時間 -->
> Completed 200 OK in 88ms (Views: 51.9ms | ActiveRecord: 4.5ms | Allocations: 21571)
```

可以看到，大約渲染出一個留言，要花 `5823 / 3 = 1941`，並且可以看到有一行有 `3 times`，那個東西代表的是你渲染東西的次數，因為今天這一篇文章有3則留言，也就是迴圈裡面有3個物件，因此會顯示 `3 times`，最終渲染該頁面的時間大約是 `21571`。



疑！？？這樣用collection的時間比普通渲染還要久欸

