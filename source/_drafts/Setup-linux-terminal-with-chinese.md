---
title: Setup linux terminal with chinese
tags: 
-linux
-note
---


Setup linux terminal with chinese
===

最近用 Vagrant 建環境時，因為下載的 Ubuntu Box 只有安裝英文語系，也就沒辦法在 Terminal 上正常顯示和輸入中文。
為避免記性差了，特以此文章做個紀錄！

## 解決步驟：

### 1. 確認目前系統安裝的語系
輸入 _locale -a_
```` 
  $ locale -a
  
  C
  C.UTF-8
  en_US.utf8
  POSIX
````
可以看到只有英文語系（C, POSIX, en_US.UTF8...等）的設定。

### 2. 確認目前語系的設定
輸入 _locale_
```` 
  $ locale
  
LANG=en_US.utf8
````
可以看到只有 **LANG** 被設定為 _en_US.UTF8_    
另外[下面](#附錄：)也附上其他的設定值。


### 3. 新增系統語系
輸入 _sudo locale-gen \<locale1\>, \<locale2\>_ ...

```
  $ sudo locale-gen zh_TW zh_TW.UTF-8
  
  Generating locales...
    zh_TW.BIG5... done
    zh_TW.UTF-8... done
  Generation complete.
 ```
或是編輯 _/var/lib/locales/supported.d/local_ 
增加想新增的語系後，輸入 _sudo locale-gen_

```
$ sudo locale-gen

en_US.UTF-8 UTF-8
zh_TW.UTF-8 UTF-8
zh_TW BIG5
```

### 4. 變更語系設定

* #### 變更系統層級的全域設定
  編輯 _/etc/default/locale_
  將  **LANG** 和 **LC_ALL** 設定為 _**zh_TW.UTF-8**_
  
  ```
   $ sudo vim /etc/default/locale
   
     LANG="zh_TW.UTF-8"
     LC_ALL="zh_TW.UTF-8"   
  ``` 
  
* #### 變更個人 User 層級的設定
  編輯 _/.bash_profile_ 等 User 設定檔
  將  **LANG** 和 **LC_ALL** 設定為 _**zh_TW.UTF-8**_
  
  ```
   $ sudo vim _/.bash_profile_
   
     export LANG="zh_TW.UTF-8"
     export LC_ALL="zh_TW.UTF-8"   
  ``` 
  
### 5. 最後
重新登入後，就可以看到 Terminal 支援中文囉！

### 附錄：

* #### 語系設定值：
  * LANG
為所有語系設定的預設值，若其他語系設定有設定值，則取代此預設值。

  * LC_ADDRESS
地址的顯示格式 e.g. _台灣, 台北_ 或是 _台北, 台灣_

  * LC_ALL
所有語系設定的設定值，可直接覆蓋其他語系設定的設定值。

  * LC_COLLATE
字串的排序方式。 e.g. 檔名字典排序

  * LC_CTYPE
字元轉換為文字或數字的設定。 e.g. 鍵盤的輸入字元轉換為文字

  * LC_IDENTIFICATION
語系資訊的 Metadata 的設定。

  * LC_MEASUREMENT
度量衡使用的單位 e.g. _公斤_/_英鎊_, _公尺_/_英尺_

  * LC_MESSAGES
系統訊息顯示的語系。

  * LC_MONETARY
貨幣使用的單位和名稱。 e.g. _NTD_, _USD_

  * LC_NAME
名字顯示的格式。 e.g. _First name_, _Last name_

  * LC_NUMERIC
數字顯示的格式。 e.g. 123.456, 123,456

  * LC_PAPER
紙張列印尺寸的設定。 e.g. A4, 11 x 17 英尺

  * LC_RESPONSE
系統回應訊息的顯示格式。 e.g. _Yes_/_No_, _y_/_n_

  * LC_TELEPHONE
電話號碼的顯示格式。

  * LC_TIME
時間和日期的顯示格式。


## _Ref_:
* [Ubuntu - Locale](https://help.ubuntu.com/community/Locale)
* [Ubuntu 14.04 主機的終端機中文顯示](http://sfs.chc.edu.tw/~chi/blog/index.php?load=read&id=296)
* [[Ubuntu] 如何設定語系locale](http://www.davidpai.tw/ubuntu/2011/ubuntu-set-locale)

###### tags: `linux`
