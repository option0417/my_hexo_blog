---
title: Weekly reading (2017/Jul 24-30)
date: 2017-07-31
tags: reading
---

## [根本就没有什么所谓的开源商业模式](http://www.ocselected.org/posts/business_model/there_is_no_open_source_business_model/)

作者翻譯了[Stephen R. Walli](https://twitter.com/stephenrwalli)對於 Open Source 是否存在 Business Model 這個問題，所提出的看法。
看來這篇後，針對參與Open Source的影響能歸納出以下幾點：

 1. 增進公司產品技術成熟度
    若將產品開源或選用Open Source軟體並參與其中，則可說是集眾人之智一同來開發、測試和維護。

 2. 節省公司成本
    文中以 [Interix](https://en.wikipedia.org/wiki/Interix) 為例，指出與其花費人力、金錢重新打造系統，不如選用熱門的Open Source軟體來得划算。

 3. 成就個人
    參與 Open Source 專案，就是是參與一個軟體專案的開發，甚至可能是世界級的，這樣的經歷比開發政府專案實在好太多！

_ref:_

 * [slide](https://www.slideshare.net/LCChina/there-is-no-open-source-business-model)
 * [原文](https://medium.com/@stephenrwalli/there-is-no-open-source-business-model-cdc4cc20238)

----

## [Upgrading Pinterest to HBase 1.2 from 0.94](https://medium.com/@Pinterest_Engineering/upgrading-pinterest-to-hbase-1-2-from-0-94-e6e34c157783)

Pinterest 是一個全球10大社群網站之一，使用者主要可以在上面分享照片和文章，也因此在服務背後的資料庫 [HBase](http://hbase.apache.org/) 保存了 10PB 以上的資料以及10M 以上的 QPS
作者主要敘述他們從HBase 0.94 到 1.2 的升級過程，包含：

 1. 如何達到 [zero downtime](https://dzone.com/articles/zero-downtime-%E2%80%93-what-it-and)
 2. 現有資料的 replication
 3. 備援/Roll back 機制
 4. HBase 效能的調整

因為目前產品使用也有使用到 HBase ，所以整篇看完特別有感，況且這樣的版本遷移也是總有一天會遇到的事情！

_ref:_

 * [AsyncHBase](http://opentsdb.github.io/asynchbase/)
 * [Thrift-Based Patch](https://issues.apache.org/jira/browse/HBASE-12814)
 * [Upgrade HBase](http://hbase.apache.org/book.html#upgrade0.96)
 * [Offheap Read-Path](https://blogs.apache.org/hbase/entry/offheap-read-path-in-production)

