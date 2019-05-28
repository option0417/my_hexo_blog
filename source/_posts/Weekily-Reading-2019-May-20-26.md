---
title: Weekly Reading (2019/May 20 ~ 26)
tags: reading
date: 2019-05-28 10:40:29
---


### 1. [redis系列--redis4.0深入持久化](https://www.cnblogs.com/wdliu/p/9377278.html)
Redis 快，但資料終究是存在記憶體裡面，還是得要有「持久化」的機制來保存重要的資料。

這篇文章就是在介紹 Redis 本身提供的「持久化」機制：
1. RDB persistent
2. AOF Persistence
3. Mixed RDB and AOP

以及觸發的時機點：
1. **save** command
2. **bgsave** command
3. **save \<second\> \<changes\>** rule
4. **Master-Slave** duplication
5. **flushall** command
6. **shutdown** command

雖說另外透過 DB 來達到持久化也是常見的作法，但若有成本考量、維運考量等情況沒有額外的 DB 下，也不失為一個不錯的辦法。

---

### 2. [Don't talk CRUD](https://codecoding.net/ruby/on/rails/2018/09/14/dont-talk-crud.html)
作者透過開發中最常見的資料操作 **C** _(Create)_ **R** _(Read)_ **U** _(Update)_ **D** _(Delete)_，說明開發者與客戶之間溝通的隔閡。

例如，對程式的會以 create 或 update 命名，但實際的功能邏輯並不只是單純的 create 和 update。

因此，作者建議透過共通的溝通方式，讓雙方能夠互相了解，也因此提到了 [DDD (Domain Driven Design)](https://en.wikipedia.org/wiki/Domain-driven_design)可作為這樣的溝通語言。

---

### 3.「我們失敗了」系列文
* [我們失敗了〈一〉- 完美的團隊也會失敗](https://kf013099.blogspot.com/2015/11/blog-post.html)
* [我們失敗了〈二〉- 天下武功，唯快不破](https://kf013099.blogspot.com/2015/11/blog-post_30.html)
* [我們失敗了〈三〉- Product/Market Fit](https://kf013099.blogspot.com/2015/12/productmarket-fit.html)
* [我們失敗了〈四〉- 軟體品質比你想像的還不重要！？](https://kf013099.blogspot.com/2015/12/blog-post.html)

簡單一句話，完美的團隊也會失敗。
對於產品，要找出「被使用者需要」的東西，而不是「讓使用者需要」。而這過程，除了 Fail Early, Fail Often 還要搶快，而搶快，也就表示對軟體的品質是要有所妥協的。 待達到 [Product/market fit](https://en.wikipedia.org/wiki/Product/market_fit) 再來調整。

---

### 4. [Web Architecture 101](https://engineering.videoblocks.com/web-architecture-101-a3224e126947)
作者以使用者發出一次 Google 搜尋的資料流為例，介紹這樣大型甚至巨型的網站架構，包含 **DNS**、**Load Balance、**Database** 等服務，都做了基本的介紹。
