---
title: Weekly Reading - 2019 Sep 09 ~ 15
tags: reading
date: 2019-09-17
---

* [別跟我稱兄道弟，我們不是一家人 : 瘋狂的 Netflix](https://vocus.cc/bass/5cd1184afd897800012a535c)

  不近人情的要求，相對也可得到豐富的報酬，各取所需罷了。

* [Is High Quality Software Worth the Cost?](https://martinfowler.com/articles/is-quality-worth-cost.html)

  作者 [Martin Fowler](https://en.wikipedia.org/wiki/Martin_Fowler_(software_engineer)) 首先將 Quality 分作 **External** 使用者能直接體會到的特性 _(ex. 好的UI , 較少Bug)_ 和 **Internal** 使用者較無法體會的特性 _(ex. 設計良好的 Software Architecture)_。

  好的 UI 設計能吸引使用者，賣得好價錢。那使用者看不到的架構設計值得追求嗎？ 答案當然是 Yes!!
  優良的設計能在同樣的品質下，增減功能。 若在不良的設計下增減功能，常常會是個悲劇。

* [谁在“谋杀” Hadoop？](https://www.infoq.cn/article/bBpKUAcd*JwLhIEVSVbD)
  因為工作，在 Hadoop 上琢磨不少時間。 文中的一段話

  ```
  除了竞争关系，这篇外媒评论文中还提到了一个重要观点，
  那就是 Hadoop 使用繁琐，用户体验糟糕，MongoDB 和 Elasticsearch 使用方便，
  而这也导致了 Hadoop 的“衰败”。
  ```

  看了心有戚戚焉，在使用 Hadoop 的確踩了不少坑。
  現在關於 Big Data 的 solution，Hadoop 已經不是唯一的選擇了。

* [Cloudflare outage caused by bad software deploy](https://blog.cloudflare.com/cloudflare-outage/)
  看似簡單的 Regular expression，也是能讓系統崩潰的... 

* [一起來了解 Web Authentication](https://blog.techbridge.cc/2019/08/17/webauthn-intro/)
  加入了實體裝置來作為驗證途徑，在現在人手一機的世界或許會是之後的趨勢，值得花時間深入研究。

* [CockroachDB: Architecture of a Geo-distributed SQL Database](https://www.infoq.com/presentations/cockroachdb-distributed-sql/)
  架構上和 [HBase](https://hbase.apache.org/) 相似，同樣有 Leadership、Replication等概念，但主要以 [Raft](https://en.wikipedia.org/wiki/Raft_(computer_science)) 作為 [consensus algorithm](https://en.wikipedia.org/wiki/Consensus_(computer_science))。
  不同的是有所謂 [Distributed Transaction](https://en.wikipedia.org/wiki/Distributed_transaction) 的功能。
  但從其流程來看，若寫入頻繁的話，效能會是個議題。
