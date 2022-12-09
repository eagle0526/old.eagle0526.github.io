---
title: Rails Self-Joins
author: YeeChen
date: 2022-12-09
category: Rails
layout: post
---



前情提要：
由於不太清楚自連結要怎麼設定，所以看完玩官方文件後，打算以自己的方式解釋他的運作原理

[官方文件](https://guides.rubyonrails.org/association_basics.html#self-joins)




在設計model的時候，你有時候會發現一個模型應該要與自身欄位有關聯。
舉個例子，你今天想要把所有員工存在一個表格中，但是你想要這張表可以追蹤上司、下屬間的關係
這種情況就可以使用到自連結



我們首先有一個Employee的model，裡面有兩個關聯
(1) 一個員工有很多的有很多的下屬，外鍵為manager_id，並且把欄位名稱設定為Employee
(2) 一個員工屬於管理者，並且把欄位名稱設定為Employee

```md
> class Employee < ApplicationRecord
>   has_many :subordinates, class_name: "Employee",
>                           foreign_key: "manager_id"
> 
>   belongs_to :manager, class_name: "Employee", optional: true
> end
```


經由剛剛上面那樣設定，我們可以得到下面兩個方法
(1) @employee.subordinates
(2) @employee.manager







