---
title: What and how about http persistent connection
date: 2017-04-08
tags:
- dev
---

![img](./imgs/connection.png)

## 前言
工作上有負責 Push 功能的開發，簡單講就是把要送給 Client 端的訊息，透過 http protocol 發送到 Google 和 Apple 的 Push Service，GCM 和 APNS。
近來，一方面為了因應越來越大的 Push 發送量；一方面也為了減少 Client 接收 Push 訊息的 latency，而開始進行調整。 首要就是先找出功能的 bottleneck，接著依照不同類型 CPU-Bound 或 IO-Bound 而有不同的調整方式。
而 IO-Bound 的部分，就先來 review 在 http protocol 和 Java 的規範上什麼是 http persistent connection。

---

## HTTP Persistent Connection
### 什麼是 HTTP Persistent Connection?
  * Allowing multiple requests and responses to be carried over a single connection.
  
### Advantages
  * Lower CPU and memory usage (because fewer connections are open simultaneously).
  * Enables HTTP pipelining of requests and responses.
  * Reduced network congestion (fewer TCP connections).
  * Reduced latency in subsequent requests (no handshaking).
  * Errors can be reported without the penalty of closing the TCP connection.

### Disadvantages
  * Resource will unavailable when connection not close well, it may may check timeout or others for ensure connection reusable.

### How to
在 HTTP 1.1 之後預設所有的 connection 都是 persistent 的，除非額外註明
`` connection: close ``
來表示 connection 會在 response 後結束。因此 **HTTP implementations SHOULD implement persistent connections.**

但在 HTTP 1.0 時並無 persistent connection 的定義，得在 header 中註明
`` connection: keep-alive ``
來表示 connection 是 persistent 的

實作 Server side 的 persistent connection 也有下列的規則來判斷，來相容不同 Client 端的 Request：
  1. If the "close" connection option is present, the connection will not persist after the current response
  2. If the received protocol is HTTP/1.1 (or later), the connection will persist after the current response
  3. If the received protocol is HTTP/1.0, the "keep-alive" connection option is present, the recipient is not a proxy, and the recipient wishes to honor the HTTP/1.0 "keep-alive" mechanism, the connection will persist after the current response
  4. The connection will close after the current response.

---

## Java HttpURLConnection
最後來看看在 Java 中如何支援 persistent connection

* Each **HttpURLConnection** instance is used to make a single request **but** the underlying network connection to the HTTP server may be **transparently shared by other instances**.

也就是說，如果透過 **HttpURLConnection** 作 http 介接的話，不用 concern 如何 persistent connection ，它會解決的！

那我們到底是不是真的能把一個 connectiob 關掉呢？
* #### Different of _close()_ and _disconnect()_
  * Calling the **close()** methods on the InputStream or OutputStream of an HttpURLConnection after a request may free network resources associated with this instance but has **no effect on any shared persistent connection**.
  * Calling the **disconnect()** method may close the underlying socket **if a persistent connection is otherwise idle at that time**.
  * HTTP header that influences connection persistence is:
  ``Connection: close``

如上所述就算直接呼叫 close() 或 disconnect() ，一樣是 JVM 會自行決定是否真的關閉 connection。

JVM 也提供了一些參數來控制 persistent connection，

* _http.keepalive (default: true)_
Indicates if persistent connections should be supported. They improve performance by allowing the underlying socket connection to be reused for multiple http requests. If this is set to true then persistent connections will be requested with HTTP 1.1 servers.

* _http.maxConnections (default: 5)_
If HTTP keepalive is enabled this value determines the maximum number of idle connections that will be simultaneously kept alive, per destination.

---

### Ref
* [HTTP persistent connection](https://medium.com/r/?url=https%3A%2F%2Fen.wikipedia.org%2Fwiki%2FHTTP_persistent_connection)
* [RFC7230](https://medium.com/r/?url=https%3A%2F%2Ftools.ietf.org%2Fhtml%2Frfc7230%23section-6.3)
* [Java HttpURLConnection and pooling](https://medium.com/r/?url=http%3A%2F%2Fstackoverflow.com%2Fquestions%2F35208950%2Fjava-httpurlconnection-and-pooling)
* [Persistent Connections](https://medium.com/r/?url=http%3A%2F%2Fdocs.oracle.com%2Fjavase%2F6%2Fdocs%2Ftechnotes%2Fguides%2Fnet%2Fhttp-keepalive.html)

