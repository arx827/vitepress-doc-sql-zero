---
title: 第 1 章 資料庫與SQL
---

# 第 1 章 資料庫與SQL
## 1-1 資料庫是什麼
  ::: details 學習重點
  - 保存了大量資料、可用電腦有效率地取用，像這樣經過加工的資料集合體就稱為「`資料庫(Database) (簡稱 DB)`」。
  - 管理資料庫的電腦資訊系統稱為「`資料庫管理系統(簡稱 DBMS)`」。
  - 運用 `DBMS` 便能讓許多人安全且方便地取用大量的資料。
  - 資料庫系統有各式各樣的類型，本書著重於「`關聯式資料庫`」，說明如何使用「`SQL`」語言來操控它。
  - 關聯式資料庫需要以「`關聯式資料庫管理系統(簡稱 RDBMS )`」執行管理工作。
  :::

### 身邊隨處可見的資料庫
  - 從固定看診的牙醫診所收到「由於前次來診已經過了半年，建議您定期做牙醫健檢」之類的明信片。
  - 在生日前1個月，從先前投宿過的旅館或飯店收到「給壽星的住宿優惠！」這樣的電子郵件。
  - 上購物網站購買商品之後，在信箱中看到「推薦商品」的電子郵件。

### 為什麼需要資料庫管理系統(DBMS)
  - 讓多人共用相同的資料
  - 擴展到處理大量的資料
  - 想要自動讀寫資料需要另外撰寫程式
  - 萬一電腦發生狀況可能失去資料
  
### DBMS具有許多類型
    按照資料的儲存形式來進行分類
  - #### 階層式資料庫 (Hierarchical Database：無特定的簡稱)
    最早存在的一種資料庫形式，以階層式結構(樹木分支的結構)來儲存、呈現資料。

  - #### 關聯式資料庫 (Relational Database：RDB)
    亦稱為 **『關係型資料庫』**，它的資料儲存方式類似Excel的工作表，以行與列所形成的二維表格形式來管理資料，比較容易理解。操作關聯式資料庫的時候，需要使用到名為 **`SQL`** (Structured Query Language：結構化查詢語言)的專用語言

    此種資料庫的DBMS被稱為 **RDBMS**(Relational Database Management System)
    - ##### 5個具有代表性的RDBMS
      | RDBMS             | 說明                                   |
      | ----------------- | ------------------------------------- |
      |**Oracle Database**|Oracle公司的RDBMS                       |
      |**SQL Server**     |Microsoft公司的RDBMS                    |
      |**DB2**            |IBM公司的RDBMS                          |
      |**PostgreSQL**     |開放原始碼 (Open Source) 的RDBMS         |
      |**MySQL**          |開放原始碼的RDBMS (2010年成為Oracle旗下產品)|

  - #### 物件導向式資料庫 (Object Oriented Database：OODB)
    物件導向語言將資料和處理資料的程序整合成名為「物件」的單位，然後利用物件完成程式的運作過程，而物件導向式資料庫正是用來儲存物件的資料庫。

  - #### XML資料庫 (XML Database：XMLDB)
    近年來，作為網路上資料交換的1種方式，名為`XML`的格式越來越普及。為了可以快速地處理大量的XML格式資料，因此發展出了此種資料庫。

  - #### 鍵值式資料儲存 (Key-Value Store：KVS)
    此類型的資料庫僅儲存由搜尋用的鍵(Key)和內容值(Value)所組成的單純資料形式，對於程式語言有些了解的讀者，可以把它想成類似「關聯陣列(Associative Array)」或「雜湊表(Hash Table)」的資料形式。可以對資料極為龐大的資料完成超高速的搜尋工作。
    
## 1-2 資料庫的架構
  ::: details 學習重點
  - RDBMS 一般採用「用戶端/伺服器型」的系統架構。
  - 對資料庫執行讀取和寫入等動作的時候，通常是從用戶端程式傳送SQL敘述至伺服器RDBMS。
  - 關聯式資料庫利用稱為「資料表」或「表」的2維表格來管理資料。
  - 資料表由代表資料項目的「行(Column，欄位)」、以及代表1筆資料的「列(Record，紀錄)」所構成，而資料讀寫的最基本單位為1列資料。
  - 行與列交會處的每個方格在本書中稱為「儲存格(Cell)」，1個儲存格當中只能放入1項資料。
  :::

### 一般 RDBMS 的系統架構
  RDBMS 所採用的系統架構，最常見的是 `用戶端 / 伺服器型 (C/S型)` 的型態。
  - **伺服器(Server)**：
    - 指能接收來自其他程式的請求，並且完成對應處理動作的服務程式(軟體)，或是安裝著這類服務程式的資訊設備(電腦)。

  - **用戶端(Client)**：
    - 對伺服器送出請求的程式(軟體)、或是安裝著這類程式的資訊設備(電腦)。
    - 用戶端程式能連接上 RDBMS 所管理的資料庫，透過 RDBMS 對資料庫中的資料執行讀取或寫入之類的動作。
    - 而用戶端的請求，主要是傳送以 `SQL 語法所寫成的敘述語法`，RDBMS 會按照 SQL 敘述的內容，回傳特定的資料、或是對資料庫中的資料執行指定的改寫動作。

### 資料表的結構
  - 關聯式資料庫的資料儲存方式有點類似 Excel 的工作表，以行與列所形成的2維表格形式來管理資料，稱為 `資料表(Table)`。
  - 資料表被保存在 RDBMS 所管理的資料庫當中，而且1個資料庫當中可以建立多個資料表。
  - 資料表縱向的`行`稱為`欄位(Column)`，用來說明這個部分儲存的是什麼資料。
  - 資料表橫向的`列`稱為`紀錄(Record)`。

  ::: warning 注意
  - 關聯式資料庫需要以列(紀錄 Record)為單位，讀取、寫入資料。
  - 1個儲存格 當中只能放入 1項資料。
  :::

## 1-3 SQL 基本概要
  ::: details 學習重點
  - SQL 是為了操作資料庫所開發出來的語言。
  - SQL 有基本的標準規格，不過各家 RDBMS 的 SQL 都略有差異。
  - 使用 SQL 的時候，需要把想執行的動作撰寫成 1段語言 (SQL 敘述)，然後傳送給 RDBMS。
  - 原則上，1段 SQL 敘述的末尾需要加上分號(；)做結束。
  - SQL 按照使用目的可分為 DDL、DML 以及 DCL。
  :::

### 標準 SQL
  - SQL (Structured Query Language) 是用來操作關聯式資料庫的語言。
  - ISO (國際標準化組織) 對SQL制訂有標準規格，而這樣作為基準的SQL 即被稱為 `標準SQL`。

### SQL 敘述與其分類
### SQL 的基本撰寫規則

## 1-4 建立資料表
### 資料表的內容
### 建立資料庫 (CREATE DATABASE 敘述)
### 建立資料表 (CREATE TABLE 敘述)
### 命名規則
### 指定資料型別
### 設定條件約束

## 1-5 刪除與修改資料表
### 刪除資料表 (DROP TABLE 敘述)
### 修改資料表結構 (ALTER TABLE 敘述)
### 新增資料至資料表

## 自我練習