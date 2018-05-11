---
title: JVM command-line utils
date: 2017-11-20
tags: dev
---

話說，當軟體過了開發衝刺的高峰後，接下來就可以開始進行 [JVM tuning](https://docs.oracle.com/cd/E13222_01/wls/docs81/perform/JVMTuning.html) 的動作了，而這時就會用到一些工具來觀察 [JVM](https://en.wikipedia.org/wiki/Java_virtual_machine) 運行的狀況。
基本上還是推薦好操作，好上手的工具來使用，例如：[VisualVM](https://visualvm.github.io/)、[Profiler](https://www.ej-technologies.com/products/jprofiler/overview.html)或至少用個 [JConsole](https://docs.oracle.com/javase/7/docs/technotes/guides/management/jconsole.html)！

但有時，天不從人願，就是會遇到只有 console 的情況... 這時就只好用 JDK 內建的 command-line 工具來觀察 JVM 了！

### 1. jps 查看目前系統上運行的JVM的 Process 資訊
我主要是用來看觀察目標的 PID，以供後續使用，僅此而已。但下面講到的 jcmd 也有這樣的功能，所以就更少用到了。

  * _jps_ &lt;argument&gt;
   * -l 條列各個JVM啟動點 main 的完整 package 資訊

---

### 2. jcmd 觀察 JVM 設定/資源和 thread 使用量
這個工具能觀察的東西就多了，例如 JVM 的系統參數、JVM 啟動參數、JVM 運行時間、載入的 Class 資訊、目前運行的 thread 資訊等等，都是在進行 tuning 時參考的資訊。

| Commands | Description | 
| ------ | ------ | 
|  Thread.print  |  Print all threads with stacktraces. **_Commonly used_** |
| GC.rotate_log | Force the GC log file to be rotated. |
| GC.class_stats | Provide statistics about Java class meta data. |
| GC.class_histogram | Provide statistics about the Java heap usage. **_Commonly used_** |
| GC.heap_dump | Generate a HPROF format dump of the Java heap. |
| GC.run_finalization | Call java.lang.System.runFinalization(). |
| GC.run | Call java.lang.System.gc(). |
| VM.uptime | Print VM uptime. |
| VM.flags | Print VM flag options and their current values. **_Commonly used_** |
| VM.system_properties | Print VM flag options and their current values. **_Commonly used_** |
| VM.command_line | Print system properties. **_Commonly used_** |
| VM.version | Print JVM version information. |
| VM.native_memory | Print native memory usage |
| ManagementAgent.stop | Stop remote management agent. |
| ManagementAgent.start_local | Start local management agent. |
| ManagementAgent.start | Start remote management agent. |


  
---

### 3. jstat 即時觀察 JVM GC的情況
最後，jstat 這項工具主要用於觀察 GC 的狀況，例如：各記憶體區塊的使用狀況、GC event 的次數、GC 花費的時間等等，透過這些資訊配合上一個 jcmd 就更容易找出 JVM 的 bottleneck。

| Option | Description | 
| ------ | ------ | 
| -class | Class loader statistics. **_Commonly used_**|
| -compiler | Java HotSpot VM Just-in-Time compiler statistics. |
| -gc | Garbage-collected heap statistics. |
| -gccapacity | Memory pool generation and space capacities. |
| -gccause |  Displays the summary of garbage collection statistics, includes the causes of the last garbage collection event and (when applicable) the current garbage collection event. |
| -gcmetacapacity | Metaspace size statistics. |
| -gcnew | New generation statistics. |
| -gcnewcapacity | New generation space size statistics. |
| -gcold | Old generation and metaspace behavior statistics. |
| -gcoldcapacity | Old generation size statistics. |
| -gcutil | Summary of garbage collection statistics. **_Commonly used_**|
| -printcompilation | Java HotSpot VM compiler method statistics. |

下面以我常用的 _-gcutil_ 來說明觀察 GC 時的參數
![gcutil](imgs/gcutil.png)
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

---
#### _ref:_ 

* [Java SE 7: Reviewing JVM Performance Command Line Tools](http://www.oracle.com/webfolder/technetwork/tutorials/obe/java/JavaJCMD/index.html)

* [jstat - Java Virtual Machine Statistics Monitoring Tool](http://docs.oracle.com/javase/1.5.0/docs/tooldocs/share/jstat.html)

* [Specific meanings of jstat parameters : YGCT FGCT GCT](https://stackoverflow.com/questions/29798704/specific-meanings-of-jstat-parameters-ygct-fgct-gct)
