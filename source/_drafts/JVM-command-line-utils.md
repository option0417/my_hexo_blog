---
title: JVM command-line utils
date: 2017-10-26 03:18:03
tags: dev
---

* ##  jps 查看目前系統上運行的JVM的資訊
 * -l 條列各個JVM啟動點 main 的完整 package 資訊

* ## jcmd 觀察 JVM 資源和 thread 使用量

* ## jstat 即時觀察 JVM GC的情況
 * -gcutil 觀察 GC 資訊
  * **S0**: Survivor space 0 記憶體使用率
  * **S1**: Survivor space 1 記憶體使用率
  * **E**:  Eden space 記憶體使用率
  * **O**:  Old space 記憶體使用率
  * **P**:  記憶體使用率
  * **YGC**: young generation GC events 次數
  * **YGCT**: Young generation GC time 
  * **FGC**: Full GC events 次數
  * **FGCT**: Full GC time in second since the JVM started
  * **GCT**: Total gc time in second since the JVM started


_ref:_ 

* [Java SE 7: Reviewing JVM Performance Command Line Tools](http://www.oracle.com/webfolder/technetwork/tutorials/obe/java/JavaJCMD/index.html)

* [jstat - Java Virtual Machine Statistics Monitoring Tool](http://docs.oracle.com/javase/1.5.0/docs/tooldocs/share/jstat.html)

* [Specific meanings of jstat parameters : YGCT FGCT GCT](https://stackoverflow.com/questions/29798704/specific-meanings-of-jstat-parameters-ygct-fgct-gct)
