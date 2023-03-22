**DO NOT READ THIS FILE ON GITHUB, GUIDES ARE PUBLISHED ON https://guides.rubyonrails.org.**

開始使用Rails
==========================

本文將介紹如何開始使用Ruby on Rails

看完本篇文章後，你將會知道：


* 如何安裝Rails、新增一個Rails應用程式和連結你應用程式的資料庫
* Rails應用程式的基本架構
* 基本的MVC架構(Model、View、Controller) 和REST架構的基本原理
* 如何快速生成Rails應用架構


--------------------------------------------------------------------------------

1、前言
-----------------


本文針對想從零開始開發Rails應用程式的初學者，不要求Rails使用經驗。

Rails是運行在Ruby程式語言上的Web應用程式框架。如果您之前沒有使用Ruby的經驗，那麼直接開始使用Rails會發現學習曲線非常陡峭。以下有多個策劃的在線學習Ruby的資源列表：

* [Official Ruby Programming Language website](https://www.ruby-lang.org/en/documentation/)
* [List of Free Programming Books](https://github.com/EbookFoundation/free-programming-books/blob/master/books/free-programming-books-langs.md#ruby)

請注意，有些資源雖然是優秀的，但涵蓋的是較舊版本的Ruby，可能不包含你在使用Rails進行日常開發中所看到的某些語法。


2、Rails是什麼？
--------------

Rails是用Ruby程式語言編寫的Web應用程序開發框架。它的設計是為了使Web應用程序開發更加容易。它允許您編寫較少的程式碼，同時實現比許多其他語言和框架更多的功能。有經驗的Rails開發人員還報告說，它使Web應用程序開發更加有趣。  


Rails 有自己的設計原則，認為問題總有一個最好的解決方法，並且有意的通過設計架構，來鼓勵用戶使用最好的解決方法，而不是使用其他替代方案。如果學習"Rails方式"，可以讓生產力大幅提升，但如果你使用Rails開發，還是依照過往寫其他語言的習慣、使用模式，你的Rails開發體驗不會太愉快。    

Rails的開發哲學包含兩個思想：    


Rails對於Web應用程式中許多事情的最佳處理方式有自己的看法，並且預設使用這組慣例，而不是通過無盡的設定文件要求您指定細節。   
   
* **不要自我重複:** DRY是軟體開發的一個原則，意思是"系統中的每個功能都要具有單一、準確、可信的實現"。不要重複書寫同一件事，寫出的程式碼才更容易維護、更具擴展性，並且也不容易出問題。  
* **慣例優於設定:** Rails對於WEB應用程式中的大多數需求都提供了最好的解決方法，並且默認使用這些慣例，而不是在無盡的設定文件中，設置每個細節。   


3、新增一個新的Rails專案
----------------------------
閱讀文件最好的方式，就是一步步跟著操作，這些步驟都是運行應用程式必須的，而且也不需要其他更多的程式碼或步驟就可以運行。     

藉由跟著本文操作，你可以創造一個叫做 `BLOG` 的Rails專案，這是一個非常簡單的部落格，在開發前，請確保已經按裝了Rails。   

備註： 文章的範例程式碼使用UNIX風格的命令提示符 `$` ，如果你的命令提示符是自定義的，看起來可能會不一樣，在Windows中，命令提示符可能類似 `C:\source_code>`。  

### 3.1 安裝Rails

安裝Rails前，你應該確認你的系統已經有安裝下面兩個東西：  

* Ruby
* SQLite3

#### 3.1.1 安裝Ruby

在 macOS 上，打開終端機；在 Windows 上，從開始菜單中選擇 `Run`，然後輸入 `cmd.exe`。任何帶有美元符號 `$` 的命令應該都在終端機中運行，確認你已經安裝當前版本的Ruby。

```bash
$ ruby --version
ruby 2.7.0
```

Rails需要 `Ruby 2.7.0` 或更高版本。建議使用最新的Ruby版本。如果版本號小於2.7.0（例如2.3.7或1.8.7），則需要安裝全新的Ruby版本。   
在Windows上安裝Rails，你應該要先安裝[Ruby Installer](https://rubyinstaller.org/)。     

更多操作系統的安裝方法請看[ruby-lang.org](https://www.ruby-lang.org/en/documentation/installation/)。   

#### 3.1.2 安裝 SQLite3

你將會需要安裝SQLite3資料庫，許多受歡迎的UNIX操作系統都帶可使用的SQLITE3版本。     
其他人可以在[SQLite3網站](https://www.sqlite.org)找到安裝說明。    

在終端機輸入下面指令，可以驗證是否已經正確安裝在並加載在 `PATH` 中：   

```bash
$ sqlite3 --version
```

這個指令會印出SQL的版本(如果有成功安裝的話)。  


#### 3.1.3 安裝Rails

要安裝Rails，請使用RubyGems提供的 `gem install` 命令：


```bash
$ gem install rails
```

要驗證是否已正確安裝所有內容，您應該能夠在終端機中運行以下指令：   

```bash
$ rails --version
```

如果印出 `Rails 7.0.0`，代表你已經準備好繼續接下來步驟。

### 3.2 新增部落格應用程式

Rails提供了很多名為 `產生器 generator` 的腳本，為了通過創建特定任務生成所需的檔案，使開發更加輕鬆。其中之一是新應用程式生成器，它將為你提供一個全新的Rails應用程式的基礎，以便你不必自己編寫它。   

要使用此生成器，打開終端機，移動到你有權創建檔案的資料夾，並運行：   


```bash
$ rails new blog
```

這指令會在 `blog` 資料夾中創建一個叫做 `Blog` 的Rails應用程式，並且使用 `bundle install` 安裝 `Gemfile` 中已經提到的 gem 依賴插件。    

提示： 你可以通過執行 `rails new --help`，來查看Rails應用程式生成器的所有命令選項。      

新增部落格應用程式後，切換到該資料夾：   


```bash
$ cd blog
```

`Blog` 資料夾將會有許多生成的檔案和資料夾，組成Rails應用程式的結構，在本教學中，大部分的工作將在 `app` 資料夾中進行。下面是Rails預設創建的每個檔案、資料夾功能的基本概述。



| 檔案/資料夾   | 作用     |
| ----------- | ------- |
|app/|包含應用程式的controller、model、view、輔助方法、信件程式和靜態資源文件，這個資料夾是本文剩餘內容關注的重點。               |
|bin/|包含用於啟動 `Rails` 腳本，以及用於安裝、更新、部署或執行應用的其他腳本。                                                 |
|config/|設定應用程式的路徑、資料庫等等。詳情請看[Configuring Rails Applications](configuring.html)。                       |
|config.ru|基於Rack的服務器所需的Rack設定，用於啟動應用程式。更多關於Rack的資訊，可以看[Rack website](https://rack.github.io/)。|
|db/|包含當前資料庫的 `schema`，以及資料庫的 `migration`。|
|Gemfile<br>Gemfile.lock|這兩個資料夾用於指定Rials應用程式所需要的gem依賴，`Bundler gem` 需要用到這兩個檔案。關於更多 Bundler 的更多資訊，請看[Bundler website](https://bundler.io)。|
|lib/|應用程式的擴展模組。|
|log/|應用程式的日誌檔案。|
|public/|包含靜態檔案和編譯過後的靜態資源。當你的應程式在執行的時候，這個資料夾將可以直接從外部被訪問。|
|Rakefile|該檔案定位並加載可在命令行中執行的任務，這些任務在Rails的各個組件中定義，如果要添加自訂義的任務，請不要修改 `Rakefile`，直接把自定義任務保存在 `lib/tasks` 資料夾中就好。|
|README.md|這是你應用程式的說明檔案，你應該要編輯此檔案讓別人知道你的應用程式怎麼使用、主要用途是幹嘛的。|
|storage/| 磁碟服務的`Active Storage`。這在[Active Storage Overview](active_storage_overview.html)有更多的介紹。|
|test/|單元測試、夾具、其他的測試裝置，詳情請看[Testing Rails Applications](testing.html)。|
|tmp/|臨時檔案 (像是快取和PID檔案)。|
|vendor/|包含第三方的程式碼。像典型的Rails應用程式中，就有第三方的 `gems`。|
|.gitattributes|此檔案定義 `git repository` 中特定路徑的元數據(metadata)，git和其他工具可以使用此元數據來增強他們的行。可以看[gitattributes documentation](https://git-scm.com/docs/gitattributes)了解更多資訊。|
|.gitignore|這個檔案告訴git他應該忽略哪些檔案(或模式)，可以看[GitHub - Ignoring files](https://help.github.com/articles/ignoring-files)了解更更忽略檔案的資訊。|
|.ruby-version|這個檔案包含Ruby預設的版本。|

Hello, Rails!
-------------

首先，我們在畫面上快速的添加一行字，為了做到這件事，我們需要執行Rails應用伺服器(就是 WEB 伺服器)。

### 3.3 啟動網路伺服器

實際上這個Rails應用程式已經可以正常運行了，要看到畫面，你需要在開發機器中，啟動WEB伺服器，你可以藉由在 `blog` 資料夾中，執行以下的指令：   

```bash
$ bin/rails server
```

備註： Windows 用戶需要把 `bin` 資料夾下的腳本文件直接傳給 Ruby 解析器，例如 `ruby bin\rails server`。   

提示： 壓縮JavaScript靜態資源需要有JavaScript執行緒，如果沒有執行緒，在壓縮靜態資源文件的時候會報 `execjs` 錯誤。一般來說 `macOS` 和 `Windows` 都已經安裝 JavaScript 執行緒。而對於 `JRuby` 用戶，建議使用 `therubyrhino` 作為執行緒，並且在 `JRuby` 生成的應用中預設添加到 `Gemfile` 中，你可以在[ExecJS](https://github.com/rails/execjs#readme)調查所有支援的執行緒。

上述命令會啟動Puma，這是Rails預設的網站伺服器，要查看運行中的應用程式，打開瀏覽器視窗，並輸入<http://localhost:3000>，這時應該會看到預設的Rails歡迎頁面：  

![Rails startup page screenshot](images/getting_started/rails_welcome.png)



當你想停止Web伺服器時，請在終端機按下Ctrl + C。在開發環境中，Rails通常不需要重新啟動伺服器；伺服器會自動捕捉你在檔案中所做的的更改。

歡迎頁面是創建Rails應用程式的 `_smoke test_` 他提供頁面，確保你的軟體已經正確設定。

### 3.4 顯示 "Hello", Rails

要讓 Rails 頁面印出 "Hello"，你至少需要新增一個 *路徑*、一個帶有 *action* 的 *controller*，以及一個 *view*，路徑將 `請求` 映射到 `controller` 中，`controller `中的 `action` 執行請求所需的工作，並準備`view`中的任何數據，最後 `view` 以所需的格式顯示數據。  

在實作方面：路徑是用 Ruby [領域特定語言（DSL）](https://en.wikipedia.org/wiki/Domain-specific_language) 所編寫。`controller`是 Ruby 的類別，他們的公開方法是 `actions`，`views` 是模板，通常是用 `HTML`、 `Ruby` 混合編寫的。  

首先在 `config/routes.rb` 中添加一個路徑到 `Rails.application.routes.draw` 區塊的頂部：  


```ruby
Rails.application.routes.draw do
  get "/articles", to: "articles#index"

  # For details on the DSL available within this file, see https://guides.rubyonrails.org/routing.html
end
```

上面的路徑設定 `GET /articles` ，會對照到 `ArticlesController` 的 `index action` 請求，  

為了創建 `ArticlesController` 及其 `index action`，我們將使用 `controller` 產生器(透過 `--skip-routes` 選項，因為我們已經有寫一個適當的路徑了。) 

```bash
$ bin/rails generate controller Articles index --skip-routes
```

接著Rails會創造數個檔案給你：
Rails will create several files for you:

```
create  app/controllers/articles_controller.rb
invoke  erb
create    app/views/articles
create    app/views/articles/index.html.erb
invoke  test_unit
create    test/controllers/articles_controller_test.rb
invoke  helper
create    app/helpers/articles_helper.rb
invoke    test_unit
```

最重要的檔案是 `controller` 檔案 `app/controllers/articles_controller.rb`。讓我們來看一下：

```ruby
class ArticlesController < ApplicationController
  def index
  end
end
```

`index action` 是空的，當一個 `action` 沒有明顯的渲染出一個 `view`(或是沒有觸發HTTP回應)，Rails將會自動渲染一個對應 `controller` 和 `action` 名稱的 `view`。 `view` 位於 `app/views` 資料夾中，所以 `index action` 預設會自動渲染這個檔案 `app/views/articles/index.html.erb`。

讓我們打開 `app/views/articles/index.html.erb`，並在裡面加上一段程式碼：

```html
<h1>Hello, Rails!</h1>
```

如果你之前停止網頁伺服器，去執行 `controller` 產生器，要記得重新輸入 `bin/rails server`，輸入完後到瀏覽器輸入 <http://localhost:3000/articles> ，這樣你就可以看到剛剛出入的 "Hello, Rails" 了。

### 3.5 設定應用程式的主頁

目前  <http://localhost:3000> 這個網址，仍然帶有Ruby on Rails標誌的頁面，我們現在也讓這個網址顯示 "Hello, Rails!"，為了做到這件事，我們來增加一個路徑，將我們應用程式的根路徑對應到適當的 `controller` 和 `action`。   

讓我們打開 `config/routes.rb` 並在 `Rails.application.routes.draw` 區塊裡面的最上方，新增一段 `root` 路徑。  

```ruby
Rails.application.routes.draw do
  root "articles#index"

  get "/articles", to: "articles#index"
end
```

現在我們當我們瀏覽 <http://localhost:3000> ，可以看到 "Hello, Rails!"，這也確定我們的 `root` 路徑有對應到 `ArticlesController` 的 `index action`。

提示： 如果想知道更多關於路徑資訊，可以看這個[Rails Routing from the Outside In](routing.html).


4、自動加載
-----------

Rails應用程式 **沒有** 使用 `require` 來加載應用程式的程式碼。   

你可以注意到 `ArticlesController` 繼承自 `ApplicationController`，但是 `app/controllers/articles_controller.rb` 沒有任何類似的 `require`。

```ruby
require "application_controller" # DON'T DO THIS.
```
應用程式類別和模組隨處可用，你不需要也不應該在 `app` 中，使用 `require` 加載任何東西。此功能稱為 `_自動加載_`，你可以在[_Autoloading and Reloading Constants_](autoloading_and_reloading_constants.html)中了解更多訊息。


你只需要在下面兩個範例中使用 `require`：

* 在 `lib` 資料夾下面加載檔案
* 加載在 `Gemfile` 中有 `require: false` 的 gem 依賴項目


5、MVC 架構
-----------

根據以下的程式碼，我們已經討論了 `路徑` 、 `controller` 、 `action`、 `view`，所有都是遵循 [MVC (Model-View-Controller)](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller) 模式的網頁應用程式組件，MVC是一種設計模式，將應用程式的職責分開，使其更容易分工合作，Rails通過慣例遵循這種設計模式。   

由於我們已經有一個 `controller` 和一個 `view` 可以使用，讓我們生成下一個組件：`模型 model`   

### 5.1 產生模型(Model)

*模型* 是用表示資料的Ruby類別，此外 `模型(Model)` 可以通過Rails的一項名為 *Active Record* 的功能與應用程式的資料庫互相作用。   

要使用model，我們會使用 `model` 生產器：   


```bash
$ bin/rails generate model Article title:string body:text
```

備註： `Model` 名稱是單數的，因為實例化模型代表單個數據紀錄，為了幫助記住這個慣例，想想你會如何呼叫模型(model)。我們都是這樣寫 `Article.new(...)` 而**不是** `Articles.new(...)`。     

這樣輸入後，會創造許多的檔案：   


```
invoke  active_record
create    db/migrate/<timestamp>_create_articles.rb
create    app/models/article.rb
invoke    test_unit
create      test/models/article_test.rb
create      test/fixtures/articles.yml
```

我們將關注的兩個檔案是 `migration` 檔案 (`db/migrate/<timestamp>_create_articles.rb`)和模型(model)檔案(`app/models/article.rb`)。  

### 5.2 資料庫遷移 Database Migrations

*Migrations* 用於改變應用程式的資料庫的結構，在Rails應用程式中，`Migrations` 是用 Ruby 撰寫的，因此他們與資料庫無關。  

讓我們看一下我們新的 `migration` 檔案：  


```ruby
class CreateArticles < ActiveRecord::Migration[7.0]
  def change
    create_table :articles do |t|
      t.string :title
      t.text :body

      t.timestamps
    end
  end
end
```

`create_table` 方法會指定說， 如何構建 `articles` 資料表。預設情況下， `create_table` 方法會設定一個 `id` 欄位作為自動遞增的主鍵，因此資料表中第一條紀錄的"ID"為1，下一條紀錄"ID"為2。   

在 `create_table` 區塊內，兩個欄位被定義為： `標題(title)` 和 `身體(body)`。這兩個是由生成器產生的，因為我們在打生成器命令的時候有加上這一段 (`bin/rails generate model Article title:string body:text`)。   

這個區塊的最後一行是對 `t.timestamps` 的呼叫。這個方法定義了另外兩個定義了另外兩個名為 `created_at` 和 `updated_at` 的欄位。正如我們看到的，當我們新增或更新模型(model)的物件時，Rails會幫我們管理這些設定值。   

讓我們根據以下的命令執行我們的 `migration`：   

```bash
$ bin/rails db:migrate
```

這個命令將會顯示資料表被成功生成：   


```
==  CreateArticles: migrating ===================================
-- create_table(:articles)
   -> 0.0018s
==  CreateArticles: migrated (0.0018s) ==========================
```

備註： 想要知道更多關於 `migrations` 的知識，可以看[Active Record Migrations](active_record_migrations.html)。   

現在我們可以使用剛剛創建的模型(model)和資料表做互動。  


### 5.3 使用Model與資料庫做互動

為了試一下Model，我們將使用Rails的一個功能 `console` ， `console` 是一個交互編碼環境，就跟IRB一樣，但他也會自動加載Rails和我們應用程式的代碼。   

讓我們使用這個命令啟動 `console` ：  

```bash
$ bin/rails console
```

你應該會看到類似 `IRB` 的指示：  

```irb
Loading development environment (Rails 7.0.0)
irb(main):001:0>
```

在這個地方，我們可以初始化一個新的 `Article` 物件：  

```irb
irb> article = Article.new(title: "Hello Rails", body: "I am on Rails!")
```

這邊最重要的是，我們在 `console` 中新增的物件，不會保存在資料庫裡面，如果你想要把物件存進資料庫，可以使用這個[`save`](https://api.rubyonrails.org/classes/ActiveRecord/Persistence.html#method-i-save):  

```irb
irb> article.save
(0.1ms)  begin transaction
Article Create (0.4ms)  INSERT INTO "articles" ("title", "body", "created_at", "updated_at") VALUES (?, ?, ?, ?)  [["title", "Hello Rails"], ["body", "I am on Rails!"], ["created_at", "2020-01-18 23:47:30.734416"], ["updated_at", "2020-01-18 23:47:30.734416"]]
(0.9ms)  commit transaction
=> true
```

上面的輸出顯示 `INSERT INTO "articles" ...` 資料庫查詢。這代表新的文章已經寫進資料表裡面，並且當我們輸入 `article`，會看到該文章的資訊：   

```irb
irb> article
=> #<Article id: 1, title: "Hello Rails", body: "I am on Rails!", created_at: "2020-01-18 23:47:30", updated_at: "2020-01-18 23:47:30">
```

`id` 、 `created_at` 和 `updated_at` 屬性是當我們儲存物件時，Rails自動幫我們設定的。   

當我們想要從資料庫得到這篇文章時，我們可以呼叫 [`find`](https://api.rubyonrails.org/classes/ActiveRecord/FinderMethods.html#method-i-find)，並傳遞 `id` 當作參數：   

```irb
irb> Article.find(1)
=> #<Article id: 1, title: "Hello Rails", body: "I am on Rails!", created_at: "2020-01-18 23:47:30", updated_at: "2020-01-18 23:47:30">
```

如果我們今天想要從資料庫找到所有的文章，我們可以呼叫[`all`](https://api.rubyonrails.org/classes/ActiveRecord/Scoping/Named/ClassMethods.html#method-i-all)方法：   

```irb
irb> Article.all
=> #<ActiveRecord::Relation [#<Article id: 1, title: "Hello Rails", body: "I am on Rails!", created_at: "2020-01-18 23:47:30", updated_at: "2020-01-18 23:47:30">]>
```

這個方法會回傳[`ActiveRecord::Relation`](https://api.rubyonrails.org/classes/ActiveRecord/Relation.html)物件，你可以把它當作一個超級陣列。   

提示： 了解更多關於模型的知識，看[Active Record Basics](active_record_basics.html)和[Active Record Query Interface](active_record_querying.html)。   

模型(Models)是MVC的最後一塊，接下來，我們要把所有部分連接起來。  

### 5.4 展示所有的文章

讓我們回到 `app/controllers/articles_controller.rb` 的 `controller` 裡面，而且順便改變 `index` 這個 `action` 的程式碼，我們這樣改，可以從資料庫抓到所有的文章：  

```ruby
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end
end
```

`view` 可以使用來自 `controller` 的實體變數，這代表我們可以在 `app/views/articles/index.html.erb` 中使用 `@articles` 這個實體變數，我們打開檔案，並把裡面的內容這樣改：  

```html+erb
<h1>Articles</h1>

<ul>
  <% @articles.each do |article| %>
    <li>
      <%= article.title %>
    </li>
  <% end %>
</ul>
```

上面的程式碼是 HTML 和 *ERB* 的混合，ERB是一個模板系統，可以分析嵌入在檔案中的Ruby代碼。在這邊，我們可以看到兩種ERB標籤：`<% %>` 和 `<%= %>`，`<% %>` 標籤代表的是，分析包含Ruby的程式碼，`<%= %>` 標籤代表的是，分析包含Ruby的程式碼，並輸出他返回的值。  

你可以把常規編寫的Ruby程式碼，都放進ERB裡面，但最好保持ERB標籤的內容簡短，方便閱讀。   


由於我們不想輸出 `@articles.each` 返回的值，我們將程式碼包在 `<% %>` 裡面，如果今天**確實**想要輸出 `article.title` 的值，會把程式碼包在 `<%= %>` 裡面。   

我們可以通過瀏覽<http://localhost:3000>頁面，看到最終結果(記得要執行`bin/rails server`)。  

根據上面做的事情後，應用程式發生了以下這些事：

1. 瀏覽器發出一個請求: `GET http://localhost:3000`
2. Rails應用程式收到一個請求
3. Rails路徑中，根目錄對應到 `ArticlesController` 的 `index action`。
4. `index action` 使用 `Article` 模型(Model) 來獲取資料庫中所有的文章。
5. Rails 自動渲染出 `app/views/articles/index.html.erb` 的畫面。
6. 分析 `view` 中的ERB程式碼，以輸出HTML檔案。
7. 伺服器將一個包含HTML的回應，發送回瀏覽器。


我們已經將所有MVC組合在一起，並且我們有了第一個 `controller` 的 `action`，接下來我們來設定第二個 `action`。  

6、文章的CRUD
--------------------------

幾乎所有的網頁應用程式都包含[CRUD (Create, Read, Update, and Delete)](https://en.wikipedia.org/wiki/Create,_read,_update,_and_delete)操作，你甚至可能會發現你應用程式所做的大部分工作都是CRUD，Rails知道這一點，並且提供許多功能來幫助簡化CRUD的流程。   

讓我們通過幫應用程式增加更多的功能，來探索這些特性。   

### 6.1 展示單篇文章

我們目前有一個 `view`，列出了我們資料庫中所有的文章，讓我們添加一個新的 `view`，來顯示單篇文章的 `title` 和 `body`。   

我們首先添加一個路徑，對應到一個新的 `controller action` 。打開 `config/routes.rb`，並在最後面加上這一條 `get "/articles/:id", to: "articles#show"`。  

```ruby
Rails.application.routes.draw do
  root "articles#index"

  get "/articles", to: "articles#index"
  get "/articles/:id", to: "articles#show"
end
```

新的路徑是另外一個 `get` 路徑，但他的路徑有一些額外的東西: `:id` 。這代表指定一個路徑的**參數**。路徑參數是請求路徑的一部分，並且可以把該值放入 `controller` 可以訪問的 `params` 中。  
例如，當處理像 `GET http://localhost:3000/articles/1` 這樣的路徑請求時， `1` 被視為 `:id` 的值，然後可以作為 `params[:id]` 在 `ArticlesController` 的 `show action` 中使用。   

現在讓我們在 `index action`  下面添加 `show action`：  

```ruby
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end

  def show
    @article = Article.find(params[:id])
  end
end
```

`show action` 使用路徑參數抓到的 `ID` 並呼叫 `Article.find` ([前面提到的](#using-a-model-to-interact-with-the-database))，返回的文章存在 `@article` 實體變數中，因此可以在 `view` 中使用這個變數，預設下， `show action` 會渲染 `app/views/articles/show.html.erb` 這個檔案。  

讓我們來新增 `app/views/articles/show.html.erb` 檔案，內容如下：   

```html+erb
<h1><%= @article.title %></h1>

<p><%= @article.body %></p>
```

現在當你瀏覽<http://localhost:3000/articles/1>這個連結，可以看到該篇文章！    

最後讓我們添加一種方便的方式來瀏覽文章的頁面，我們將 `app/views/articles/index.html.erb` 中每篇文章的標題，連結到他的個別文章頁面：  

```html+erb
<h1>Articles</h1>

<ul>
  <% @articles.each do |article| %>
    <li>
      <a href="/articles/<%= article.id %>">
        <%= article.title %>
      </a>
    </li>
  <% end %>
</ul>
```

### 6.2 路徑資源 Resourceful Routing

到目前為止，我們已經介紹了 CRUD 的 "R" (讀取)，我們最終會寫到 "C"(新增)、"U"(更新)、"D"(刪除)，正如你可能猜到的那樣，我們將通過添加新的`路徑`、`controller action`和`view`，來實現其他的CUD。
每當我們將`路徑`、`controller action`和`view`組合在一起，來對物件執行CRUD操作時，我們會稱該物件為 *resource*。例如：在我們的應用程式中，我們會說一篇文章是一種資源。

Rails提供了一種叫做 [`resources`](https://api.rubyonrails.org/classes/ActionDispatch/Routing/Mapper/Resources.html#method-i-resources)的路徑方法，他對應了一個集合所有常規的路徑資源，例如：文章。因此，在我們繼續實作"C"、"U"和"D"之前，讓我們用 "resources" 替換 `config/routes.rb` 中的兩個 `get` 路徑設定。  

```ruby
Rails.application.routes.draw do
  root "articles#index"

  resources :articles
end
```

我們可以在終端機輸入這個指令 `bin/rails routes` 來查看我們目前有哪些路徑：   

```bash
$ bin/rails routes
      Prefix Verb   URI Pattern                  Controller#Action
        root GET    /                            articles#index
    articles GET    /articles(.:format)          articles#index
 new_article GET    /articles/new(.:format)      articles#new
     article GET    /articles/:id(.:format)      articles#show
             POST   /articles(.:format)          articles#create
edit_article GET    /articles/:id/edit(.:format) articles#edit
             PATCH  /articles/:id(.:format)      articles#update
             DELETE /articles/:id(.:format)      articles#destroy
```


`resources` 方法還設定了 URL 和 路徑輔助方法，我們可以使用它們來避免我們的程式碼依賴特定的路徑設定。   
例如： `article_path` 輔助程式在給定文章返回 `"/articles/#{article.id}"`。   

我們可以用他來整理 `app/views/articles/index.html.erb` 中的連結：  

上面的"前綴"列中的值加上 `_url` 或 `_path` 等等後綴，就可以構成這些輔助方法的名稱。  

```html+erb
<h1>Articles</h1>

<ul>
  <% @articles.each do |article| %>
    <li>
      <a href="<%= article_path(article) %>">
        <%= article.title %>
      </a>
    </li>
  <% end %>
</ul>
```

我們將通過 [`link_to`](https://api.rubyonrails.org/classes/ActionView/Helpers/UrlHelper.html#method-i-link_to) 這個輔助方法， `link_to` 助手渲染出一個連結，第一個參數是該連結的文字，第二個參數是連結的目的地。如果我們將Model的物件當作第二個參數，`link_to` 將會呼叫適當的路徑，幫助程式將物件轉換成路徑。  

例如：如果我們有一篇文章， `link_to` 會呼叫 `article_path`，所以 `app/views/articles/index.html.erb` 會變成：  

```html+erb
<h1>Articles</h1>

<ul>
  <% @articles.each do |article| %>
    <li>
      <%= link_to article.title, article %>
    </li>
  <% end %>
</ul>
```


提示： 想要知道更多路徑的知識，看[Rails Routing from the Outside In](routing.html)。  

### 6.3 新增一篇新的文章

現在我們來實作CRUD的"C"(新增)。通常在WEB應用程式中，創建新資源是一個多步驟的過程，首先，用戶填寫表單，然後用戶提交表單。如果沒有錯誤，那麼資源就會被創建，並顯示某種確認。否則，表單將顯示錯誤訊息，並重複該過程。

在Rails應用程式中，這些步驟通常由 `controller` 的 `new` 和 `create` 的 `action` 處理。讓我們在 `app/controllers/articles_controller.rb` 中的 `show action` 下添加這些 `action` 來實作創建功能：  

```ruby
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end

  def show
    @article = Article.find(params[:id])
  end

  def new
    @article = Article.new
  end

  def create
    @article = Article.new(title: "...", body: "...")

    if @article.save
      redirect_to @article
    else
      render :new, status: :unprocessable_entity
    end
  end
end
```

`new` 的 `action` 通常會實例化一篇新文章，但不會保存他。這篇文章將在構建表單時用於 `view` 中，預設情況下， `new` 動作會渲染在 `app/views/articles/new.html.erb`，接下來我們新增這個檔案。

`create` 動作將實例化一個新文章，並為 `title` 和 `body` 設定值，並嘗試儲存他，如果文章成功儲存，則操作將重導到文章頁面 `"http://localhost:3000/articles/#{@article.id}"`。儲存失敗的話，會通過渲染 `app/views/articles/new.html.erb` 頁面，並帶有狀態碼[422 Unprocessable Entity](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/422)來重新顯示表單。這裡的 `title` 和 `body` 是虛擬值，在創建表單之後，我在再回來修改他們。   

備註： [`redirect_to`](https://api.rubyonrails.org/classes/ActionController/Redirecting.html#method-i-redirect_to) 會讓瀏覽器傳一個新的請求。 而 [`render`](https://api.rubyonrails.org/classes/AbstractController/Rendering.html#method-i-render) 會渲染目前請求的一個 `view`，在更改資料庫或應用程式狀態後，使用 `redirect_to` 很重要，否則如果用戶刷新頁面，瀏覽器會發出同樣的請求，並且重複觸發請求。  


#### 6.3.1 使用表單生成器


我們將使用 Rails 一個稱為 *form builder* 的功能來創建我們的表單。使用表單生成器，我們可以用最簡短的程式碼，來生成一個遵守 Rails 慣例的表單。
讓我們用以下的內容創建 `app/views/articles/new.html.erb`：   

```html+erb
<h1>New Article</h1>

<%= form_with model: @article do |form| %>
  <div>
    <%= form.label :title %><br>
    <%= form.text_field :title %>
  </div>

  <div>
    <%= form.label :body %><br>
    <%= form.text_area :body %>
  </div>

  <div>
    <%= form.submit %>
  </div>
<% end %>
```

[`form_with`] 輔助方法實例化一個表單生成器。在我們呼叫的 `form_with` 區塊中，像 [`label`](https://api.rubyonrails.org/classes/ActionView/Helpers/FormBuilder.html#method-i-label) 和[`text_field`](https://api.rubyonrails.org/classes/ActionView/Helpers/FormBuilder.html#method-i-text_field)這樣的方法，可以在表單構建器上輸出適當的表單元素。  

`form_with` 呼叫的結果輸入如下所示：

```html
<form action="/articles" accept-charset="UTF-8" method="post">
  <input type="hidden" name="authenticity_token" value="...">

  <div>
    <label for="article_title">Title</label><br>
    <input type="text" name="article[title]" id="article_title">
  </div>

  <div>
    <label for="article_body">Body</label><br>
    <textarea name="article[body]" id="article_body"></textarea>
  </div>

  <div>
    <input type="submit" name="commit" value="Create Article" data-disable-with="Create Article">
  </div>
</form>
```

提示： 想知道更多表單構建器的資訊，看[Action View Form Helpers](form_helpers.html)。   

#### 6.3.2 使用強參數

提交的表單數據，連同捕獲的路徑參數，將放入 `params` Hash表中，。因此，`create` 動作可以通過 `params [:article] [:title]` 存取提交的標題，通過 `params [:article] [:body]` 存取提交的正文。我們可以將這些值逐個傳遞給`Article.new`，但這將變得冗長且可能出現錯誤。而且，隨著我們添加更多的字段，情況只會變得更糟。  

因此，我們將傳遞一個包含這些值的單個Hash。但是，我們仍然必須指定該Hash表中允許的值。否則，惡意用戶可能提交額外的表單字串並覆蓋私有數據。實際上，如果我們直接將未經過濾的 `params [:article]` Hash傳遞給 `Article.new`，Rails將引發 `ForbiddenAttributesError` 以警告我們有關該問題。因此，我們將使用Rails的一個名為 *Strong Parameters* 的功能來過濾params。把它看作是 `params` 的[強類型化]（https://en.wikipedia.org/wiki/Strong_and_weak_typing）。   

讓我們在位於 `app/controllers/articles_controller.rb` 底部的私有方法中添加 `article_params`，該方法過濾 `params`。讓我們更改 `create` 來使用它:  

```ruby
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end

  def show
    @article = Article.find(params[:id])
  end

  def new
    @article = Article.new
  end

  def create
    @article = Article.new(article_params)

    if @article.save
      redirect_to @article
    else
      render :new, status: :unprocessable_entity
    end
  end

  private
    def article_params
      params.require(:article).permit(:title, :body)
    end
end
```

提示： 要了解更多關於強參數的資訊，請參見[Action Controller 概述  § Strong Parameters](action_controller_overview.html#strong-parameters)。  


#### 6.3.3 驗證和展示錯誤訊息

正如我們所看到的，創建資源是一個由多個步驟構成的過程。處理無效的用戶輸入是該過程的另一步。Rails 提供了一個名為「驗證」（validations）的功能，以幫助我們處理無效的用戶輸入。驗證是在模型對象保存之前檢查的規則。如果任何檢查失敗，則保存將被中止，並且適當的錯誤消息將被添加到模型(Model)物件的 `errors` 屬性中。   

讓我們在 `app/models/article.rb` 中為我們的模型(Model)添加一些驗證：   

```ruby
class Article < ApplicationRecord
  validates :title, presence: true
  validates :body, presence: true, length: { minimum: 10 }
end
```

第一個驗證代表必須存在`title`值。因為`title`是一個字串，這意味著`title`值必須包含至少一個非空格字符。   

第二個驗證代表必須存在一個`body`值。此外，它還規定`body`值必須至少有10個字符長度。  

備註：您可能想知道`title`和`body`屬性在哪定義的。Active Record會自動為每個欄位定義模型(Model)屬性，因此你不需要在模型(Model)檔案中聲明這些屬性。  

有了驗證，讓我們修改`app/views/articles/new.html.erb`來顯示`title`和`body`的任何錯誤消息：  



```html+erb
<h1>New Article</h1>

<%= form_with model: @article do |form| %>
  <div>
    <%= form.label :title %><br>
    <%= form.text_field :title %>
    <% @article.errors.full_messages_for(:title).each do |message| %>
      <div><%= message %></div>
    <% end %>
  </div>

  <div>
    <%= form.label :body %><br>
    <%= form.text_area :body %><br>
    <% @article.errors.full_messages_for(:body).each do |message| %>
      <div><%= message %></div>
    <% end %>
  </div>

  <div>
    <%= form.submit %>
  </div>
<% end %>
```

[`full_messages_for`](https://api.rubyonrails.org/classes/ActiveModel/Errors.html#method-i-full_messages_for) 方法返回指定屬性的 "使用者" 錯誤陣列訊息，如果該屬性沒有錯誤，則陣列為空。     

為了理解如何協同工作，讓我們再次查看 `new` 和 `create` 的 `controller actions`：   

```ruby
  def new
    @article = Article.new
  end

  def create
    @article = Article.new(article_params)

    if @article.save
      redirect_to @article
    else
      render :new, status: :unprocessable_entity
    end
  end
```

當我們瀏覽 <http://localhost:3000/articles/new> 網址時，`GET /articles/new` 請求是對應到 `new` 的 `action`。 `new action` 不嘗試儲存 `@article`。因此，驗證不會被檢查，也不會出現錯誤訊息。  

當我們提交表單時，`POST /articles` 請求對應到 `create` 動作。`create` 動作會嘗試儲存 `@article`。因此，驗證將會被檢查。如果任何驗證失敗，`@article` 將不會被保存，並且會用包含錯誤訊息的 `app/views/articles/new.html.erb` 重新渲染。  

提示：要了解有關驗證的更多信息，請參閱 [Active Record Validations](active_record_validations.html)。要了解有關驗證錯誤訊息的更多信息，請參閱 [Active Record Validations § Working with Validation Errors](active_record_validations.html#working-with-validation-errors)。   

#### 6.3.4 最後 Finishing Up

我們現在可以通過瀏覽<http://localhost:3000/articles/new>頁面，來創建新的文章，最後讓我們從 `app/views/articles/index.html.erb` 的底部超連結，連接到該頁面。  

```html+erb
<h1>Articles</h1>

<ul>
  <% @articles.each do |article| %>
    <li>
      <%= link_to article.title, article %>
    </li>
  <% end %>
</ul>

<%= link_to "New Article", new_article_path %>
```

### 6.4 更新文章

我們已經完成了CRUD中的"CR"部分。現在讓我們繼續進行"U"(更新)操作。更新資源(resource)與創建資源非常相似，它們都是很多步驟的過程。首先，用戶請求編輯數據的表單。然後，用戶提交表單。如果沒有錯誤，則更新資源。否則，表單將顯示錯誤消息，並重複該過程。  

這些步驟通常由 `controller` 的 `edit` 和 `update` 的 `action` 處理。讓我們在 `app/controllers/articles_controller.rb` 的 `create` 動作下方添加這些 `action` 來實作更新功能：   

```ruby
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end

  def show
    @article = Article.find(params[:id])
  end

  def new
    @article = Article.new
  end

  def create
    @article = Article.new(article_params)

    if @article.save
      redirect_to @article
    else
      render :new, status: :unprocessable_entity
    end
  end

  def edit
    @article = Article.find(params[:id])
  end

  def update
    @article = Article.find(params[:id])

    if @article.update(article_params)
      redirect_to @article
    else
      render :edit, status: :unprocessable_entity
    end
  end

  private
    def article_params
      params.require(:article).permit(:title, :body)
    end
end
```


注意，`edit` 和 `update` 的 `action` 類似於 `new` 和 `create` 的 `action`。    

`edit` 的 `action` 從資料庫中取得文章，並將其存在 `@article` 中，以便在構建表單時使用。預設下， `edit` 的 `action` 將渲染 `app/views/articles/edit.html.erb` 這個頁面。   

`update` 的 `action` 從資料庫中重新獲得文章，並嘗試由 `article_params` 過濾的提交表單數據來更新他。如果沒有驗證失敗，並且更新成功，則 `action` 將瀏覽器重導到文章頁面，否則將重新渲染 `app/views/articles/edit.html.erb` 這個頁面，並帶有錯誤訊息。  


Notice how the `edit` and `update` actions resemble the `new` and `create`
actions.   

#### 6.4.1 使用 Partials 共享 View 程式碼


我們的 `edit` 表單看起來跟 `new` 表單差不多，多虧了 Rails 表單生成器的厲害之處，即使兩個檔案的程式碼一樣，表單構建器也會發出對應的請求，而他發出的請求會以模型(Model)的物件是否已經保存來傳請求。  

由於程式碼將相同，因此我們將其抽取出來，建立一個名為*partial*的共享 `view`。讓我們創建 `app/views/articles/_form.html.erb` ，其內容如下：    

```html+erb
<%= form_with model: article do |form| %>
  <div>
    <%= form.label :title %><br>
    <%= form.text_field :title %>
    <% article.errors.full_messages_for(:title).each do |message| %>
      <div><%= message %></div>
    <% end %>
  </div>

  <div>
    <%= form.label :body %><br>
    <%= form.text_area :body %><br>
    <% article.errors.full_messages_for(:body).each do |message| %>
      <div><%= message %></div>
    <% end %>
  </div>

  <div>
    <%= form.submit %>
  </div>
<% end %>
```

上面的代碼與 `app/views/articles/new.html.erb` 中的表單相同，不同之處在於所有的 `@article` 都被替換成了 `article`。
由於局部視圖是共享代碼，最好的做法是它們不要依賴於控制器操作設置的特定實例變量。相反，我們將作為本地變量將文章傳遞給局部視圖。

讓我們通過 [`render`] (https://api.rubyonrails.org/classes/ActionView/Helpers/RenderingHelper.html#method-i-render) 更新 `app/views/articles/new.html.erb` 使用該局部視圖：


以上的程式碼跟 `app/views/articles/new.html.erb` 中的表單相同，不同之處在於所有的 `@article` 都被替換成了 `article` ，由於 `局部 view` 是共享程式碼，最好的做法是他們不要依賴於 `controller action` 設定的特定實體變數。相反的，我們用區域變數傳給 `局部view`。  

讓我們通過 [`render`] (https://api.rubyonrails.org/classes/ActionView/Helpers/RenderingHelper.html#method-i-render) 更新 `app/views/articles/new.html.erb` 使用該局部view：  

```html+erb
<h1>New Article</h1>

<%= render "form", article: @article %>
```

備註： 部分檔案名稱必須前綴 **帶著** 下劃線，e.g. `_form.html.erb`。但是當你渲染的時後，他被引用是沒有下劃線的，e.g. `render "form"`。     

現在，讓我創建一個非常相似的 `app/views/articles/edit.html.erb`：  

```html+erb
<h1>Edit Article</h1>

<%= render "form", article: @article %>
```

提示： 要了解更多關於 `partials` 的資訊，看[Layouts and Rendering in Rails § Using Partials](layouts_and_rendering.html#using-partials)。  


#### 6.4.2 最後 Finishing Up

我們現在可以通過瀏覽其編輯頁面（例如`<http：//localhost：3000 / articles / 1 / edit>`）來更新文章。最後，讓我們在 `app/views/articles/show.html.erb` 的底部連結到編輯頁面。  

```html+erb
<h1><%= @article.title %></h1>

<p><%= @article.body %></p>

<ul>
  <li><%= link_to "Edit", edit_article_path(@article) %></li>
</ul>
```

### 6.5 刪除文章

接著，我們來到 CRUD 的 "D"(刪除)。刪除資源比創建或更新更簡單。只需要一個路徑和一個 `controller action`。而我們的資源路徑（`resources :articles`）已經提供了路徑，它將 `DELETE / articles/:id` 請求對應到 `ArticlesController` 的 `destroy` `action` 。    

因此，讓我們在 `app/controllers/articles_controller.rb` 中添加一個 `destroy action` ，在 `update action` 下面：  

```ruby
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end

  def show
    @article = Article.find(params[:id])
  end

  def new
    @article = Article.new
  end

  def create
    @article = Article.new(article_params)

    if @article.save
      redirect_to @article
    else
      render :new, status: :unprocessable_entity
    end
  end

  def edit
    @article = Article.find(params[:id])
  end

  def update
    @article = Article.find(params[:id])

    if @article.update(article_params)
      redirect_to @article
    else
      render :edit, status: :unprocessable_entity
    end
  end

  def destroy
    @article = Article.find(params[:id])
    @article.destroy

    redirect_to root_path, status: :see_other
  end

  private
    def article_params
      params.require(:article).permit(:title, :body)
    end
end
```

`destroy` 的 `action` 從資料庫中獲取文章並在其上呼叫[`destroy`](https://api.rubyonrails.org/classes/ActiveRecord/Persistence.html#method-i-destroy)。  
然後，它使用狀態程式碼[303 See Other](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/303)重導瀏覽器到根路徑。      

我們選擇重導到根路徑，因為那是我們主要瀏覽文章的入口，但在其他情況下，你可能會選擇重導到 `articles_path`。      

現在讓我們在 `app/views/articles/show.html.erb` 底部增加一個連結，以便我們可以從文章頁面刪除一篇文章：      

```html+erb
<h1><%= @article.title %></h1>

<p><%= @article.body %></p>

<ul>
  <li><%= link_to "Edit", edit_article_path(@article) %></li>
  <li><%= link_to "Destroy", article_path(@article), data: {
                    turbo_method: :delete,
                    turbo_confirm: "Are you sure?"
                  } %></li>
</ul>
```

在上面的程式碼中，我們使用 "data" 選項來設置 `Destroy` 連結的 `data-turbo-method` 和 `data-turbo-confirm` HTML屬性。這兩個屬性都與 Turb​​o (https://turbo.hotwired.dev/) 綁定，Turb​​o已經包含在新的Rails應用程式中。 `data-turbo-method ="delete"` 將使該連結進行 `DELETE` 請求，而不是 `GET` 請求。 `data-turbo-confirm ="Are you sure?"` 會在點擊連結時顯示確認對話框。如果用戶取消對話框，請求將被中止。   

就是這樣！我們現在可以列出、顯示、創建、更新和刪除文章了！   


7、增加第二個模型(Model)
---------------------

是時候幫應用程式增加第二個模型(Model)了，第二個模型(Model)將處理文章的評論。   

### 7.1 產生模型(Model)

我們將看到與建立 `Article` 模型時使用過的相同生成器。這次我們將創建一個 `Comment` 模型來保存對文章的評論。在終端機中執行此命令：   

```bash
$ bin/rails generate model Comment commenter:string body:text article:references
```

這個指令會產生以下四個檔案：   


| 檔案                                          | 用途                                                                                                   |
| -------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| db/migrate/20140120201010_create_comments.rb | 用於在資料庫創建評論的 `migration` 檔案(你的檔案名會包含不同的時間戳記)                                         |
| app/models/comment.rb                        | Comment的模型(model)檔案                                                                                |
| test/models/comment_test.rb                  | Comment模型的測試檔案                                                                                    |
| test/fixtures/comments.yml                   | 用於測試的comment夾具                                                                                    |


首先看一下 `app/models/comment.rb` 檔案：  

```ruby
class Comment < ApplicationRecord
  belongs_to :article
end
```

這與你之前看到的 `Article` 模型(Model)非常相似。不同之處在於 `belongs_to：article` 這一行，他設定了 `Active Record` 的 `關聯`。你將在本指南的下一節中學習一些關於關聯的知識。   

在終端機中使用 (`:references`) 關鍵字是模型的特殊數據類型。他在你的資料表上創鍵一個新的，帶有附加模型名稱和 `_id` 的整數直列。之後通過分析 `db/schema.rb` 檔案，可以更好的理解這些內容。     

除了模型(model)之外，Rails還創建了一個 `migration` ，用於創建相應的資料表。  

```ruby
class CreateComments < ActiveRecord::Migration[7.0]
  def change
    create_table :comments do |t|
      t.string :commenter
      t.text :body
      t.references :article, null: false, foreign_key: true

      t.timestamps
    end
  end
end
```

`t.references` 這行程式碼創建 `article_id` 整數字串，為了這個字串建立索引，並建立指向 `articles` 表的 `id` 字段的外鍵約束。接著執行下面的指令：  

```bash
$ bin/rails db:migrate
```

Rails很聰明，只會針對當前資料庫還沒有運行過的 `migration` 進行遷移，運行結果向下面：   

```
==  CreateComments: migrating =================================================
-- create_table(:comments)
   -> 0.0115s
==  CreateComments: migrated (0.0119s) ========================================
```

### 7.2 關聯模型(Models)

`Active Record` 關聯讓我們可以輕易的建立兩個模型(Model)之間的關係。對於評論和文章，我們可以像下面這樣聲明：  

* 每一條評論都屬於一個文章
* 一篇文章可以有很多條評論

實際上，這種表達方式和 Rails 用於建立模型(Model)關聯的句法非常接近。前文我們已經看過 Comment 模型(Model)中 `(app/models/comment.rb)`，用於建立每一條評論都屬於某一篇文章：   

```ruby
class Comment < ApplicationRecord
  belongs_to :article
end
```

你將會需要到 `app/models/article.rb` 這個檔案新增另外的關聯：  

```ruby
class Article < ApplicationRecord
  has_many :comments

  validates :title, presence: true
  validates :body, presence: true, length: { minimum: 10 }
end
```

這兩個聲明啟用了很多自動行為。例如，如果你有一個包含文章的實體變數 `@article`，你可以使用 `@article.comments` 檢索屬於該文章的所有評論，以作為一個陣列的形式。   
提示： 有關 `Active Record` 關聯的更多訊息，請看[Active Record 關聯](association_basics.html)指南。  

### 7.3 增加評論的路徑

與 `articles` 的 `controller` 一樣，我們需要添加一個路徑，以便Rails知道我們想要導航到哪裡查看 `comments`。再次打開 `config/routes.rb` 檔案，並按照以下方式編輯：   

```ruby
Rails.application.routes.draw do
  root "articles#index"

  resources :articles do
    resources :comments
  end
end
```

這會在 `articles` 中創建 `comments` 為一個嵌套資源。建立文章和評論之間存在的階層關係。     

提示：有關路徑的更多信息，請參閱 [Rails Routing](routing.html) 指南。    


### 7.4 產生控制器 Controller

有了模型(model)，下面應該創建對應的 `controller`：   

```bash
$ bin/rails generate controller Comments
```

這個指令會創建三個檔案和一個空資料夾：   

| 檔案/資料夾                                    | 用途                                     |  
| -------------------------------------------- | ---------------------------------------- |
| app/controllers/comments_controller.rb       | 評論的控制器 controller                    |
| app/views/comments/                          | 控制器 controller 的 view 在這             |
| test/controllers/comments_controller_test.rb | 控制器 controller 的 test 檔案             |
| app/helpers/comments_helper.rb               | view 的 輔助方法檔案                       |



在部落格中，讀者將在閱讀文章後直接創建自己的評論，一旦添加了評論，他們將被送回文章展示頁面，以查看現在列出的評論。因此，我們的 `CommentsController` 提供了一種創建評論和在垃圾評論到達時刪除評論的方法。因此，首先，我們將連接文章展示模板（`app/views/articles/show.html.erb`），以讓我們發表新評論。   

首先，修改顯示文章的模板 (`app/views/articles/show.html.erb`)，添加發表評論的功能：  

```html+erb
<h1><%= @article.title %></h1>

<p><%= @article.body %></p>

<ul>
  <li><%= link_to "Edit", edit_article_path(@article) %></li>
  <li><%= link_to "Destroy", article_path(@article), data: {
                    turbo_method: :delete,
                    turbo_confirm: "Are you sure?"
                  } %></li>
</ul>

<h2>Add a comment:</h2>
<%= form_with model: [ @article, @article.comments.build ] do |form| %>
  <p>
    <%= form.label :commenter %><br>
    <%= form.text_field :commenter %>
  </p>
  <p>
    <%= form.label :body %><br>
    <%= form.text_area :body %>
  </p>
  <p>
    <%= form.submit %>
  </p>
<% end %>
```

這在 `Article` 展示頁面上添加了一個表單，通過呼叫 `CommentsController` 的 `create action` 來創建新評論。這裡的 `form_with` 呼叫使用一個陣列，它將構建一個嵌套路徑，例如 `/articles/1/comments`。   

讓我們在 `app/controllers/comments_controller.rb` 中設定 `create` 的 `action`：  

```ruby
class CommentsController < ApplicationController
  def create
    @article = Article.find(params[:article_id])
    @comment = @article.comments.create(comment_params)
    redirect_to article_path(@article)
  end

  private
    def comment_params
      params.require(:comment).permit(:commenter, :body)
    end
end
```


上面的程式碼比 `Articles` 的 `controller` 程式碼複雜的多，這是你設定嵌套的副作用，對於每一個發表評論的請求，都必須記錄這條評論屬於哪篇文章，因此需要在 `Article` 的 `Model` 上呼叫 `find方法` 來獲取文章物件。   

此外，程式碼利用了一些關聯特有的方法。在 `@article.comments` 上 呼叫create方法來創建和保存評論。同時自動把評論和對應的文章關聯起來。   

添加評論後，我們使用 `article_path(@article)` 輔助方法把用戶倒回原本的頁面，如前文所述，這裡呼叫了 `ArticlesController` 的 `show action` 來渲染 `show.html.erb模板`，因此需要修改 `app/views/articles/show.html.erb` 檔案來顯示評論：  


```html+erb
<h1><%= @article.title %></h1>

<p><%= @article.body %></p>

<ul>
  <li><%= link_to "Edit", edit_article_path(@article) %></li>
  <li><%= link_to "Destroy", article_path(@article), data: {
                    turbo_method: :delete,
                    turbo_confirm: "Are you sure?"
                  } %></li>
</ul>

<h2>Comments</h2>
<% @article.comments.each do |comment| %>
  <p>
    <strong>Commenter:</strong>
    <%= comment.commenter %>
  </p>

  <p>
    <strong>Comment:</strong>
    <%= comment.body %>
  </p>
<% end %>

<h2>Add a comment:</h2>
<%= form_with model: [ @article, @article.comments.build ] do |form| %>
  <p>
    <%= form.label :commenter %><br>
    <%= form.text_field :commenter %>
  </p>
  <p>
    <%= form.label :body %><br>
    <%= form.text_area :body %>
  </p>
  <p>
    <%= form.submit %>
  </p>
<% end %>
```

現在可以在我們的部落格中幫文章添加評論了，評論添加後就會顯示在正確的位置上了。  

![Article with Comments](images/getting_started/article_with_comments.png)   


8、重構
-----------

現在部落格的文章和評論都已經正常運行了，打開 `app/views/articles/show.html.erb` 的檔案，會看到檔案程式碼變得又長又不美觀，因此下面我們要用 `partials view` 來重構程式碼。  

### 8.1 view 局部渲染

首先新增評論的局部 `view`，把顯示文章評論的程式碼抽出來，新增 `app/views/comments/_comment.html.erb` 檔案，添加下面的程式碼：  

```html+erb
<p>
  <strong>Commenter:</strong>
  <%= comment.commenter %>
</p>

<p>
  <strong>Comment:</strong>
  <%= comment.body %>
</p>
```


然後你可以像下面那樣，改變 `app/views/articles/show.html.erb` 檔案的內容：   

```html+erb
<h1><%= @article.title %></h1>

<p><%= @article.body %></p>

<ul>
  <li><%= link_to "Edit", edit_article_path(@article) %></li>
  <li><%= link_to "Destroy", article_path(@article), data: {
                    turbo_method: :delete,
                    turbo_confirm: "Are you sure?"
                  } %></li>
</ul>

<h2>Comments</h2>
<%= render @article.comments %>

<h2>Add a comment:</h2>
<%= form_with model: [ @article, @article.comments.build ] do |form| %>
  <p>
    <%= form.label :commenter %><br>
    <%= form.text_field :commenter %>
  </p>
  <p>
    <%= form.label :body %><br>
    <%= form.text_area :body %>
  </p>
  <p>
    <%= form.submit %>
  </p>
<% end %>
```


這樣對於 `@article.comments` 集合中的每條評論，都會渲染 `app/views/comments/_comment.html.erb` 檔案中的局部 `view`。`render` 方法會遍歷 `@article.comments` ，把每條評論賦值給局部view中的同名區域變數，也就是這裡的 `comment變數`。   

### 8.2 渲染局部表單

讓我們也將新的評論部分移到它自己的 partial 中。再次創建一個名為 `app/views/comments/_form.html.erb` 的檔案，其中包含：   

```html+erb
<%= form_with model: [ @article, @article.comments.build ] do |form| %>
  <p>
    <%= form.label :commenter %><br>
    <%= form.text_field :commenter %>
  </p>
  <p>
    <%= form.label :body %><br>
    <%= form.text_area :body %>
  </p>
  <p>
    <%= form.submit %>
  </p>
<% end %>
```

然後到這個 `app/views/articles/show.html.erb` 檔案，像下面一樣修改：   

```html+erb
<h1><%= @article.title %></h1>

<p><%= @article.body %></p>

<ul>
  <li><%= link_to "Edit", edit_article_path(@article) %></li>
  <li><%= link_to "Destroy", article_path(@article), data: {
                    turbo_method: :delete,
                    turbo_confirm: "Are you sure?"
                  } %></li>
</ul>

<h2>Comments</h2>
<%= render @article.comments %>

<h2>Add a comment:</h2>
<%= render 'comments/form' %>
```


上面程式碼中第二個 render 方法的參數就是我們剛剛定義的 `comments/form` 局部 view，Rails很聰明。能夠發現字串中的斜線，會知道我們想渲染 `app/views/comments` 資料夾中的 `_form.html.erb` 檔案。  

`@article` 是實體變數，因此在所有局部view中都可以使用。  


### 8.3 使用關注點 Concerns


Concern是讓 `controller` 和 `model` 更容易理解和管理的一種方式。當多個 `Model` 或 `controller` 共享相同的 `concerns` 時，也具有重複使用的優點。`Concerns` 是使用模塊實現的，這些模塊包含表示 `Model` 或 `Controller` 負責定義明確的功能片段方法。在其他語言中，模塊通常被稱為mixins。      

你可以在 `controller` 或 `model` 中使用 `concern`，就像使用任何模塊一樣。當你最初使用 `rails new blog` 創建應用程式時，除其他資料夾外， `app/` 內還創建了兩個資料夾：  


```
app/controllers/concerns
app/models/concerns
```

在下面的範例中，我們將為我們的部落格實做一個新功能，它將受益於使用關注點(concern)。然後，我們將創建一個關注點(concern)，並重構代碼以使用它，使代碼更DRY且易於維護。    

部落格文章可能具有不同的狀態 - 例如，它可能對所有人都可見(即`public`)，或者只對作者可見(即`private`)。它也可能被隱藏，但仍可檢索(即`archived`)。評論也可以是隱藏的或可見的。可以使用每個 `Model` 中的 `status` 來表示這一點。  

首先，讓我們運行以下 `migration` 以將 `status` 添加到 `Articles` 和 `Comments` 之中：  

```bash
$ bin/rails generate migration AddStatusToArticles status:string
$ bin/rails generate migration AddStatusToComments status:string
```

接著，我們用剛生成 `migration` 來更新資料庫：  

```bash
$ bin/rails db:migrate
```

要幫現有的文章和評論改變狀態，你可以在生成的 `migration` 檔案中添加 `default:"public"` 選項，然後再次啟動 `migration`。你還可以在Rails Console中呼叫 `Article.update_all（status：“public”）` 和 `Comment.update_all（status：“public”）`。  

提示： 要了解更多有關 migrations 的訊息，請看[Active Record Migrations](active_record_migrations.html)。   

我們還必須在 `app / controllers / articles_controller.rb` 中作為強參數允許 `：status` 鍵。   


```ruby
  private
    def article_params
      params.require(:article).permit(:title, :body, :status)
    end
```
然後在 `app/controllers/comments_controller.rb` 檔案的強參數也是：   

```ruby
  private
    def comment_params
      params.require(:comment).permit(:commenter, :body, :status)
    end
```

在 `article` 模型(model)中，當你使用 `bin/rails db:migrate` 指令，來執行 `migration` 增加 `status` 欄位後。你可以增加：  

```ruby
class Article < ApplicationRecord
  has_many :comments

  validates :title, presence: true
  validates :body, presence: true, length: { minimum: 10 }

  VALID_STATUSES = ['public', 'private', 'archived']

  validates :status, inclusion: { in: VALID_STATUSES }

  def archived?
    status == 'archived'
  end
end
```

`Comment` 的 model 也是：  


```ruby
class Comment < ApplicationRecord
  belongs_to :article

  VALID_STATUSES = ['public', 'private', 'archived']

  validates :status, inclusion: { in: VALID_STATUSES }

  def archived?
    status == 'archived'
  end
end
```

然後，在我們文章的 `index action` 模板中(`app/views/articles/index.html.erb`) ，我們將使用 `archived?` 方法來避免顯示任何已經存檔的文章：  

```html+erb
<h1>Articles</h1>

<ul>
  <% @articles.each do |article| %>
    <% unless article.archived? %>
      <li>
        <%= link_to article.title, article %>
      </li>
    <% end %>
  <% end %>
</ul>

<%= link_to "New Article", new_article_path %>
```

同樣地，在我們的評論 `局部 view`（`app/views/comments/_comment.html.erb`）中，我們將使用 `archived？` 方法來避免顯示任何已存檔的評論：   

```html+erb
<% unless comment.archived? %>
  <p>
    <strong>Commenter:</strong>
    <%= comment.commenter %>
  </p>

  <p>
    <strong>Comment:</strong>
    <%= comment.body %>
  </p>
<% end %>
```

然而，如果你再看看我們的模型(model)，你會發現邏輯是重複的。如果將來我們增加部落格其他的功能 - 比如包括私人消息 - 我們可能會再次重複這個邏輯。這就是關注點很有用的地方。    

一個關注點只負責模型(model)職責的一個集中子集; 我們關注點中的方法都與模型的可見性(visible)有關。讓我們稱我們的新關注點（模塊）為`可見(Visible)`。我們可以在`app/models/concerns`中創建一個名為`visible.rb`的新檔案，並儲存在模型(model)中重複的所有狀態方法。   


`app/models/concerns/visible.rb`
```ruby
module Visible
  def archived?
    status == 'archived'
  end
end
```


我們可以將狀態驗證新增到 concern 中，但這稍微複雜一些，因為驗證是在類別層級上呼叫的方法。而 `ActiveSupport::Concern` （[API 指南](https://api.rubyonrails.org/classes/ActiveSupport/Concern.html)）提供了一種更簡單的引入它們的方式。  

```ruby
module Visible
  extend ActiveSupport::Concern

  VALID_STATUSES = ['public', 'private', 'archived']

  included do
    validates :status, inclusion: { in: VALID_STATUSES }
  end

  def archived?
    status == 'archived'
  end
end
```

現在，我們可以從每個模型(model)中刪除重複的邏輯，而且引入我們新的 `Visible` 模組：   


In `app/models/article.rb`:

```ruby
class Article < ApplicationRecord
  include Visible

  has_many :comments

  validates :title, presence: true
  validates :body, presence: true, length: { minimum: 10 }
end
```

在 `app/models/comment.rb` 這個檔案也要引入：  

```ruby
class Comment < ApplicationRecord
  include Visible

  belongs_to :article
end
```

在 `concerns` 中也可以添加類別方法，如果我們想要在主頁顯示公開文章或評論的次數，我們可以將一個類別方法添加到 `Visible` 中，如下所示：  

```ruby
module Visible
  extend ActiveSupport::Concern

  VALID_STATUSES = ['public', 'private', 'archived']

  included do
    validates :status, inclusion: { in: VALID_STATUSES }
  end

  class_methods do
    def public_count
      where(status: 'public').count
    end
  end

  def archived?
    status == 'archived'
  end
end
```

然後在 `view` 中，你可以像其他類別方法一樣呼叫他：   

```html+erb
<h1>Articles</h1>

Our blog has <%= Article.public_count %> articles and counting!

<ul>
  <% @articles.each do |article| %>
    <% unless article.archived? %>
      <li>
        <%= link_to article.title, article %>
      </li>
    <% end %>
  <% end %>
</ul>

<%= link_to "New Article", new_article_path %>
```


最後，我們將在表單中添加一個選擇框，讓用戶在創建新文章或發布新評論時選擇狀態。我們還可以將默認狀態指定為 `公共 public`。在 `app/views/articles/_form.html.erb` 中，我們可以添加：  

```html+erb
<div>
  <%= form.label :status %><br>
  <%= form.select :status, ['public', 'private', 'archived'], selected: 'public' %>
</div>
```

然後在 `app/views/comments/_form.html.erb` 這個檔案可以改成這樣：  

```html+erb
<p>
  <%= form.label :status %><br>
  <%= form.select :status, ['public', 'private', 'archived'], selected: 'public' %>
</p>
```

9、刪除評論
-----------------

部落格的另一個重要特點是能夠刪除垃圾評論。為此，我們需要在 `view` 中新增一個連結，並在 `CommentsController` 新增 `destroy` 的 `action`。   

因此，首先讓我們在 `app/views/comments/_comment.html.erb` 局部文件中添加刪除連結：   

```html+erb
<% unless comment.archived? %>
  <p>
    <strong>Commenter:</strong>
    <%= comment.commenter %>
  </p>

  <p>
    <strong>Comment:</strong>
    <%= comment.body %>
  </p>

  <p>
    <%= link_to "Destroy Comment", [comment.article, comment], data: {
                  turbo_method: :delete,
                  turbo_confirm: "Are you sure?"
                } %>
  </p>
<% end %>
```

點擊這個新的「刪除評論」連結會觸發一個 `DELETE /articles/:article_id/comments/:id` 到我們的 `CommentsController`，這可以讓我們找到我們要刪除的評論，因此讓我們在我們的控制器中（`app/controllers/comments_controller.rb`）添加一個 `destroy` 的 `action`。   

```ruby
class CommentsController < ApplicationController
  def create
    @article = Article.find(params[:article_id])
    @comment = @article.comments.create(comment_params)
    redirect_to article_path(@article)
  end

  def destroy
    @article = Article.find(params[:article_id])
    @comment = @article.comments.find(params[:id])
    @comment.destroy
    redirect_to article_path(@article), status: :see_other
  end

  private
    def comment_params
      params.require(:comment).permit(:commenter, :body, :status)
    end
end
```

`destroy` 的 `action` 首先找到指定文章，然後在 @article.comments 集合中找到指定評論，接著從數據庫刪除這條評論，最後重導到顯示文章的頁面。  

### 9.1 刪除關聯對象

如果要刪除一篇文章，文章的相關評論也需要刪除，否則這些評論還會佔用資料庫的空間，在 Rails 中可以使用關聯的 `dependent` 選項來完成這一個工作，像下面這樣修改 `app/models/article.rb` 檔案中的 `Article` 模型(Model)：  


```ruby
class Article < ApplicationRecord
  include Visible

  has_many :comments, dependent: :destroy

  validates :title, presence: true
  validates :body, presence: true, length: { minimum: 10 }
end
```

10、安全
--------

### 10.1 基本身份驗證

如過我們把部落格放到網站上。任何人都能夠新增、修改、刪除文章或刪除評論(CRUD)。   

Rails 提供了一個非常簡單的 HTTP 身份驗證系統，可以很好的解決這個問題。   

我們需要一種方法來禁止未認證用戶訪問 `ArticlesController` 的 `action`，這裡我們使用 `http_basic_authenticate_with` 方法，通過這個方法的認證後，才能訪問所請求的 `action`。   

要使用這個身份認證系統，可以在 `app/controllers/articles_controller` 檔案中的 `ArticlesController` 頂部進行設定。這裡除了 `index` 和 `show` 的 `action`，其他 `action` 都要通過身份認證才能訪問，為此要像下面這樣添加程式碼：   


```ruby
class ArticlesController < ApplicationController

  http_basic_authenticate_with name: "dhh", password: "secret", except: [:index, :show]

  def index
    @articles = Article.all
  end

  # snippet for brevity
```

我們同時希望只有通過身份驗證的用戶才能刪除評論，為此要在 `CommentsController` (`app/controllers/comments_controller.rb`) 中像下面這樣添加程式碼：


```ruby
class CommentsController < ApplicationController

  http_basic_authenticate_with name: "dhh", password: "secret", only: :destroy

  def create
    @article = Article.find(params[:article_id])
    # ...
  end

  # snippet for brevity
```

現在如果我們嘗試新增一篇文章，你會看到 HTTP 基本身份驗證對話筐：   

![Basic HTTP Authentication Challenge](images/getting_started/challenge.png)

輸入正確的用戶名、密碼後，你將保持身份驗證狀態，直到需要不同的用戶名和密碼或關閉瀏覽器。   

其他的身份驗證方法，Rails中還有兩個受歡迎的身份驗證外掛[Devise](https://github.com/plataformatec/devise)、[Authlogic](https://github.com/binarylogic/authlogic)。  

### 10.2 其他安全注意事項

安全，尤其是網站應用的安全，是一個非常廣泛的領域，關於Rails應用安全更多的介紹，請看這個[Ruby on Rails Security Guide](security.html)。   


11、接下來要做什麼？
------------

現在你已經看到了你的第一個Rails應用程式，你可以隨意更新它並進行自己的實驗。  

請記住，你不必在沒有幫助的情況下做所有的事情。當你在實作Rails時，請隨時諮詢這些支援資源：  

* The [Ruby指南](index.html)
* The [Ruby信件列表](https://discuss.rubyonrails.org/c/rubyonrails-talk)



12、設定問題
---------------------


在 Rails 中，儲存外部數據最好都使用 UTF-8 編碼。虽然 Ruby 資料庫和 Rails 通常都能將使用其他編碼的外部數據轉換為 UTF-8 編碼，但並非總是可靠的，所以最好還是確保所有的外部數據都使用 UTF-8 編碼。  

編碼出錯的最常見的狀況是在瀏覽器中出現帶有問號的的黑色菱形塊，另一個狀況是本該出`ü`字串的地方出现了`Ã¼`字串。Rails 內部採取了許多步驟来解決常見、可以自動檢測和糾正的編碼問題。儘管如此，如果不使用 UTF-8 編碼来儲存外部數據，偶而還是會出現無法自動檢測和糾正的編碼問題。   

下面是非 UTF-8 編碼數據的兩種常見來源：

* 文本編輯器：大多數的文本編輯器（例如 TextMate）預設使用 UTF-8 編碼保存檔案。如果你的文本編輯器未使用 UTF-8 編碼，就可能導致在模板中輸入的特殊字串（例如 `é`）在瀏覽器中顯示為帶有問號的黑色菱形塊。這個問題也會出现在 `i18n` 翻譯文件中。大多數未預設使用 UTF-8 編碼的文本編輯器（例如 Dreamweaver 的某些版本）提供了將預設編碼修改為 UTF-8 的方法，别忘了進行修改。   

* 資料庫：預設情况下，Rails 會把從資料庫中取出的資料轉換成 UTF-8 格式。儘管如此，如果資料庫內部不使用 UTF-8 編碼，就有可能無法保存用戶輸入的所有字串。例如，如果資料庫內部使用 Latin-1 編碼，而用户輸俄語、希伯来語或日語字串，那麼在把資料保存到資料庫時就會造成資料永久丟失。因此，如果可能的話，就請在資料庫內部使用 UTF-8 編碼。   

