---
title: Dom vs SAX vs StAX
date: 2018-07-19 02:13
tags: dev
---

之前有個 side-project 需要針對 XML 進行解析，也趁此機會好好整理一下
在 Java 上，三種不同的解析 XML Document 的方法。


## [DOM](https://en.wikipedia.org/wiki/Document_Object_Model)
會針對要解析的 XML Document 建立完整的 DOM Tree (如下圖)

 ![dom_tree](https://upload.wikimedia.org/wikipedia/commons/5/5a/DOM-model.svg)

 * ### 優點：
   * 可對建立好的 DOM Tree 隨意存取任何一個節點
 * ### 缺點：
   * 若 XML Document 過大，則會耗費過多的 Memory，甚至發生無法預期的錯誤，例如： [OOM](https://en.wikipedia.org/wiki/Out_of_memory)
   * 建立 DOM Tree 的時間花費，可能也會是個效能瓶頸。

## [SAX](https://en.wikipedia.org/wiki/Simple_API_for_XML)
透過 Event-Driven 和 Push-model ，依序將 XML Document 的 Element 一個個 push 到繼承自 DefaultHandler 的自定義 Handler 來解析
 * ### 優點：
    * 較 Dom 方法快速許多
    * 較 Dom 方法節省 Memory

 * ### 缺點：
    * 無法隨意存取任何一個節點
    * 若要讀取先前的節點資料，須自行保存

## [StAX](https://en.wikipedia.org/wiki/StAX)
基本上跟 SAX 同樣都是透過 Event-Driven，但是用 Pull-model 來存取解析 XML Document。

 * ### 優點：
    * 較 Dom 方法快速許多
    * 較 Dom 方法節省 Memory

 * ### 缺點：
    * 無法隨意存取任何一個節點
    * 若要讀取先前的節點資料，須自行保存



### 我的選擇...
最後選擇的是 StAX 來解析 XML Document，一方面 Event-Driven 消能表現比較好，也節省 Memory。 另一方面，不像 SAX 還得先實做對應的 Handler，在 Pull-model 實作上比較直覺，因為就像 iterate Collection 那樣的方式。

### _ref_:
* [Java Dom Parser, tutorialspoint](https://www.tutorialspoint.com/java_xml/java_dom_parser.htm)
* [Java SAX Parser, tutorialspoint](https://www.tutorialspoint.com/java_xml/java_sax_parser.htm)
* [Java StAX Parser, tutorialpoint](https://www.tutorialspoint.com/java_xml/java_stax_parser.htm)
* [Java SAX vs. StAX, Jenkov.com](http://tutorials.jenkov.com/java-xml/sax-vs-stax.html)
