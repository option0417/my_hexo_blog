---
title: Weekly Reading (2021 Apr26~May02)
date: 2021-05-04
tags: reading
---

### [深度解读：Kafka 放弃 ZooKeeper，消息系统兴起二次革命](https://www.infoq.cn/article/phf3gfjutdhwmctg6kxe)

原本 Kafka 必須依賴 ZooKeeper 來完成分散式的控制，但在 Kafka 的 v2.8.0 版本後拿掉了對 ZooKeeper 依賴，改以內建的 Kafka Raft Quorum 來控制。

而這麼做的主要原因是，Kafka 和 ZooKeeper 都是分散式系統，隨著系統成長眾多節點之間的交互構通，越來越複雜，進而嚴重影響效能。而 Kafka 的 Scalability 亦會被 ZooKeeper 所限制。

因上述原因，Kafka 團隊自行開發基於 Raft 共識演算法的 KRaft Quorum 來替代 使用 ZAB 的 ZooKpeer。

其結果，效能大幅提升，在一個有 200萬 patition 的 Cluster 中，Shutdown 到 Recover 的時間，可由數分鐘的進步到只需 30 秒。
而系統建置的需求也明顯降低，原本需要 6 個節點 (3 個供 Kafka、3 個供 ZooKpeer)，現在也只需要 3 個節點即可。

  * Ref:
[1. Apache Kafka Made Simple: A First Glimpse of a Kafka Without ZooKeeper](https://www.confluent.io/blog/kafka-without-zookeeper-a-sneak-peek/)
