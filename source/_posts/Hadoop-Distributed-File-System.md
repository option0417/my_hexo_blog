---
title: Hadoop Distributed File System
tags:
  - paper
  - big data
date: 2017-04-11 22:59:38
---

# The Hadoop Distributed File System

## Introduction
在 Hadoop 架構中，較熱門、常見的都是上層的計算應用，例如 MapReduce、Hive、Pig、Spark、Mahout 等等。但這些應用其中有一個重要的元素，就是在底層的分散式資料儲存 HDFS！
而在 2010 年左右，Yahoo!就已在 production 上以 25000 台server 建構運行了多個 cluster，其中儲存了 25 PB的資料。而最大的 cluster 包含將近 3500 台server。


## Architecture
在 HDFS 的架構上，每個 cluster 係由 1 個 NameNode 和 多個 DataNode 所組成。並將資料分作 metadata 和 application data 各自儲存在 NameNode 和 DataNode 上，並透過 replication 的方式來達到資料的 reliability。

* ### NameNode
主要儲存了一份稱作 **Namespace** 的檔案結構，就像是檔案路徑 _root_dir/sub_dir_/file_ 由 file 和 directories 所組成並以階層的方式呈現，
其中儲存了包含 permissions、modification、access times、namespace 和 disk space quotas 這類 metadata。
NameNode 會將 Namespace 存在記憶體中，稱作 **image**；而 image 修改歷程的資料則稱作 **journal**；亦可將 image 存於底層檔案系統作 persistent，稱作 **check-point**。
實際的檔案內容，被切分為預設 128 MB(可調整) 大小的 **block** 來作為最小的資料單元，而分散的 replicate 到各個 DataNode 上，
而 NameNode 會維護一份 namespace tree 和一份各個 block 各自放在哪個 DataNode 實體路徑的 mapping table。
讀取檔案時，Client 端會先到 NameNode 取得擁有所需 data block 而且最近的 DataNode 位置。
寫入檔案時，Client 端會先到 NameNode 取得三個 DataNode 的位置後，再將 data block 寫到這三個 DataNode

* ### DataNode
  * ####  Namespace ID / Storage ID
在每個 HDFS 的 cluster 中，會有唯一的 Namespace ID，用來確認 cluster 中的 NameNode 和 DataNode 是管理和儲存同一份資料和結構。<br>
DataNode 在第一次啟動時，會向設定的 NameNode 進行 handshake 來**取得**該 cluster 的 Namespace ID。
DataNode 非第一次啟動時，會向設定的 NameNode 進行 handshake 來**驗證**該 cluster 的 Namespace ID 和自己的是否相同。<br>
DataNode 和 NameNode 進行的 handshake 中也會**驗證**雙方的軟體版本，
如果 Namespace ID 或軟體版本不同的話，DataNode 都會自動關機，因為若 Namespace ID 不同，則可能雙方儲存的資料跟結構都不同；若軟體版本不同，則可能對資料處理的方式不同，造成錯誤。<br>
Handshake 結束後，就表示 DataNode 和 NameNode 互相註冊了，DataNode 會產生唯一的 **Storage ID** 作為後續和 NameNode 溝通使用。

  * #### Data block / Block report
每個儲存在 DataNode 上的 **Data Block** 會分作兩個檔案儲存在本地端的 native 檔案系統，第一個檔案存放資料本體；第二個檔案存放 metadata 包含checksums 和 時間戳記。 _(P.S Data Block 所佔的檔案大小依其實際儲存的資料而定，非固定)_<br>
DataNode 則透過 **Block report** 告訴 NameNode 它存了哪塊 Data block，它的 block id、建立時間、block 長度。
Block report 除了在 DataNode 啟動後送出第一次後，後面則每小時發送一次。

  * #### Heartbeats
DataNode 每隔3秒會發送一次 heartbeats 給 NameNode，裡面夾帶 _總共可使用的空間大小_ 、_目前已使用的空間大小_ 和 _目前有多少個正在進行的檔案傳輸_，
這些資訊都能讓 NameNode 作爲空間使用和Load blance 的決策考量。
NameNode 如果10分鐘內沒收到 heartbeats 的話，會將 DataNode 視為離線，且準備啟動 replicas 作業將離線 DataNode 上的 Data block 複製到還在線上的 DataNodes。<br> 因為 NameNode 不主動和 DataNode 連線，所以會在 heartbeats 的 response 中夾帶下列命令來進行管理：
 * replicate blocks to other nodes
 * remove local block replicas
 * re-register or to shut down the node
 * send an immediate block report
 
* ### HDFS Client
* ### Image and Journal
* ### Checkpoint Node
* ### Backup Node
* ### Upgrades, File System Snapshots

## FILE I/O OPERATIONS AND REPLICA MANGEMENT
* ### File Read and Write
* ### Block Placement
* ### Replication management
* ### Balancer
* ### Block Scanner
* ### Decommissioing
* ### Inter-Cluster Data Copy

### _ref_: 
[The Hadoop Distributed File System](http://storageconference.us/2010/Papers/MSST/Shvachko.pdf)