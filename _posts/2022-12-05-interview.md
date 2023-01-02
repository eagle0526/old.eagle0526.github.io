---
title: 面試題
author: YeeChen
date: 2022-12-05
category: Rails
layout: post
---

1、JavaScript
------


### 1-1、跨來源資源分享 CORS Cross
> --  
> 跨來源資源共用（Cross-Origin Resource Sharing (CORS)）  
> 是一種使用額外 HTTP 標頭令目前瀏覽網站的使用者代理 (en-US)取得存取其他來源（網域）伺服器特定資源權限的機制。  
> 當使用者代理請求一個不是目前文件來源——例如來自於不同網域（domain）、通訊協定（protocol）或通訊埠（port）的資源時，  
> 會建立一個跨來源 HTTP 請求（cross-origin HTTP request）。   
> [CORS (Cross-Origin Resource Sharing)](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/CORS)  
> from MDN  
> --  
{: .block-tip}


#### 1-1-1、同源、非同源到底是什麼意思？


簡單地說，用 JavaScript 存取資源時，如果是同源的情況下，存取不會受到限制  
**那同源的定義是什麼呢？**  

所謂的同源，必須滿足以下三個條件：  
(1) 相同的通訊協定 (protocol)，即 http/https    
(2) 相同的網域 (domain)   
(3) 相同的通訊埠 (port)   



#### 1-1-2、跨來源請求  

不是同源的情況下，就會產生一個跨來源 http 請求（cross-origin http request）。
而跨來源請求就必須遵守CORS的規範



#### 1-1-3、CORS簡介
簡單地說，CORS (Cross-Origin Resource Sharing) 是針對不同源的請求而定的規範   
透過 JavaScript 存取非同源資源時，server 必須明確告知瀏覽器允許何種請求   
只有 server 允許的請求能夠被瀏覽器實際發送，否則會失敗。    



#### 1-1-4、非同源解決方法
(1) 如果對方沒有開 CORS policy 是抓不回來的  
(2) 如果未來碰到業主網站CORS的問題，打電話叫他們開  
(3) CORS policy test 可以檢測對方CORS有沒有開  

> --  
> **CORS是針對瀏覽器的行為，而不是針對JavaScript**  
> 這個行為就是指，假設你今天想從網頁存取別人的個人資料，會碰到資安問題  
> 如果未來有第二個可以控制瀏覽器的語言，這個語言也會碰到CORS的問題  
> --  
{: .block-tip}



#### 1-1-5、CORS proxy

1. 另外架一個伺服器 (用ruby node python)，去抓對方網站資料  
2. 然後因為伺服器是我們自己的，可以把該伺服器的 CORS 打開   
3. 就可以用我們自己的JavaScript把那台伺服器的資料抓過來   



> --  
> [CORS參考資料連結](https://shubo.io/what-is-cors/#%E5%90%8C%E6%BA%90%E6%94%BF%E7%AD%96-same-origin-policy)  
> --  
{: .block-tip}



### 1-2、物件繼承
(1) Q. All objects have prototype?      
Ans. false  
詳解：是所有function都有prototype，所有物件都有的是__proto__    

(2) 箭頭函式沒有prototype

(3) 使用new實體時，在類別裡面呼叫return，會發生啥事

```md
> function Cat(name) {
>     this.name = name
>     return 123             -> 如果今天刻意給實體 return  (正常人不會在這邊return)
> }
> 
> const c = new Cat("cc")    -> 實際上會忽略上面傳下來的123，一樣是傳Cat下來
> console.log(c)             # 印出 Cat { name: 'cc' }
```


2、Ruby On Rails
------

### 2-1、find vs find_by vs find_by!
> ---  
> **面試題**
> Book.find      => find如果錯誤，會噴出錯誤警告，而且find後面只能接數字  
> Book.find_by   => find_by錯誤，只會給一個nil，find_by後面可以接其他的欄位  
> Book.find_by!  => Exception，加一個驚嘆號就如果錯誤的話，就會跳錯誤警告給你  
> ---  
{: .block-tip}




### 2-2、do...end VS {}
> --  
> Q. do...end、{}兩種block哪邊不一樣  
> Ans.  
> 結合率強度不同，do...end的結合率強度比較低，像是加號，{}的強度比較強，像是乘號  
> 強度比較弱會發生什麼事，會變成被p搶走  
> --  
{: .block-tip}  



### 2-3、SQL injection(注入)是什麼  
> --  
> **面試題**  
> Q. SQL injection(注入)是什麼  
> A. 也稱SQL隱碼或SQL注碼，是發生於應用程式與資料庫層的安全漏洞。  
> 簡而言之，是在輸入的字串之中夾帶SQL指令，在設計不良的程式當中忽略了字元檢查，  
> 那麼這些夾帶進去的惡意指令就會被資料庫伺服器誤認為是正常的SQL指令而執行，因此遭到破壞或是入侵。  
> --  
{: .block-tip}




### 2-4、include與extend的差別在哪裡


include是引用模組內的方法來擴充實體方法，而extend則是擴充類別方法。

#### 2-4-1、舉個例子

先創造兩個模組，一個是Ball，一個是Eat
```ruby
module Ball
  def play_baseball
    puts 'I play baseball'
  end
end

module Eat
  def lunch
    p 'I eat lunch'
  end
end
```
接著把創造一個Human類別，並分別引入兩個模組
```ruby
class Human
  include Ball
  extend Eat
end

man = Human.new
man.play_baseball           # I play baseball
man.lunch                   # 噴錯
Human.lunch                 # I eat lunch
```

#### 2-4-2、回答面試官
include與extend都是可以讓類別增加方法的做法，而差別在於include是增加實體方法，而是extend增加類別方法。





### 2-5、說明private的特色




### 2-6、gem、bundle差異

gem版本介紹、和bundle有什麼不一樣、Gemfile.lock是用來做啥的  

#### 2-6-1、gem版本代表的意思  
設計多版本的原因是，如果今天加小物件，跳patch版號，如果今天是加新功能，跳minor版號，如果大更新，跳major版號  

```md
> gem 'xxx' 3.1.7
> 3 => major => 完全不同的產品  
> 1 => minor => 有可能會壞掉    
> 7 => patch => 增加不太重要的功能 （可以隨便更新來用）

> gem 'xxx', '~> 3.1.7' 3.2.0 不會裝
> gem 'xxx', '>3.1.7' 3.2.0 會裝
```

> --  
> ~的意思是，會去裝比較安全的版本，所以今天如果改動的是patch就會安裝，跳minor版號就不會安裝  
> --  
{: .block-tip}

### 2-6-2、gem vs bundle  

(1) gem 是一次裝一個指定的套件  
(2) bundle 是一次下載寫在 gemfile 的描述檔  

```md
> bundle指令會做以下事情

> (1) 找 gemfile  
> (2) gem install ...  
> (3) 產生 Gemfile.lock  
```
  
### 2-6-3、Gemfile.lock是啥

假設今天A套件需要B套件2.0版本，C套件需要B套件3.0版本，bundle完後，可以解決上面這個問題        
```md
> Gemfile.lock => 會產生一個“多個檔案相依性”的檔案，這可以解決版本不同的相依性問題  
```




3、Repl(Read-eval-print loop)是啥
------
### wiki
「讀取-求值-輸出」循環（英語：Read-Eval-Print Loop，簡稱REPL）  
也被稱做交互式頂層構件（英語：interactive toplevel），是一個簡單的，交互式的編程環境。  
這個詞常常用於指代一個Lisp的交互式開發環境，也能指代命令行的模式。  
  
### 懶人包
REPL對於學習一門新的程式語言具有很大的幫助，因為它能立刻對初學者做出回應。  
  




4、SQL
------

### 4-1、SQL、NoSQL的差異

|差異|關聯式資料庫|NoSQL 資料庫|
|:-:|:-:|:-:|
|最佳工作負載|關聯式資料庫專門用於交易性以及高度一致性的線上交易處理 (OLTP) 應用程式，並且非常適合於線上分析處理 (OLAP) 使用。|NoSQL 資料庫專門用於包含低延遲應用程式的多樣資料存取模式。NoSQL 搜尋資料庫專門用於進行半結構資料的分析。|
|資料模型|關聯式模型將資料標準化，成為由列和欄組成的表格。結構描述嚴格定義表格、列、欄、索引、表格之間的關係，以及其他資料庫元素。此類資料庫強化資料庫表格間的參考完整性。|NoSQL 資料庫提供鍵值、文件和圖形等多種資料模型，具有最佳化的效能與規模。|
|效能|一般而言，效能取決於磁碟子系統。若要達到頂級效能，通常必須針對查詢、索引及表格結構進行優化。	|效能通常會受到基礎硬體叢集大小、網路延遲，以及呼叫應用程式的影響。|
|擴展|	關聯式資料庫通常透過增加硬體運算能力向上擴展，或以新增唯讀工作負載複本的方式向外擴展。|NoSQL 資料庫通常可分割，因為存取模式可透過使用分散式架構來向外擴展，以近乎無限規模的方式提供一致效能來增加資料吞吐量。|
|API|存放和擷取資料的請求是透過符合結構式查詢語言 (SQL) 的查詢進行通訊。這些查詢是由關聯式資料庫剖析和執行。|以物件為基礎的 API 讓應用程式開發人員可輕鬆存放和擷取資料結構。應用程式可透過分區索引鍵查詢鍵值組、欄集，或包含序列化應用程式物件與屬性的半結構化文件。|



### 4-2 資料庫中的ACID屬性是什麼

關聯式資料庫則提供單元性、一致性、隔離性和耐用性 (ACID) 的屬性
(1) 單元性要求交易完整執行或完全不執行。  
(2) 一致性要求進行交易時資料就必須符合資料庫結構描述。  
(3) 隔離性要求並行的交易必須分開執行。  
(4) 耐用性要求從意外的系統故障還原成上個已知狀態的能力  


> ---  
> NoSQL 資料庫通常透過鬆綁部分關聯式資料庫的 ACID 屬性來取捨以達到能夠橫向擴展的更彈性化資料模型。  
> 這使得 NoSQL 資料庫成為橫向擴展超過單執行個體上限的高吞吐量、低延遲使用案例的最佳選擇  
> ---  
{: .block-tip}