---
title: What and how of the HTTP Cache - 基本應用
date: 2018-10-09
tags: 
 - dev
 - cache
 - http
---

這陣子因為工作的關係跟 Cache 有了接觸的機會，從系統底層一直到網路的傳輸多少都有些涉略，也因此想將這陣子所學做些整理。
首先本文想先介紹 HTTP 的 Cache 機制，其主要目的，簡單講就是減少 Client 端 (主要為 Browser)與 Server 端之間的資料傳輸的次數和資料量。

下面就來針對 HTTP 1.0/1.1 的 Cache 機制作個就介紹。


## HTTP 1.0
在 HTTP 1.0 時就有提供 [_**Expires**_](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.21)、[_**Pragma**_](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.32)、[**Last-Modified**](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.29) 和 [**If-Modified-Since**](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.25) 這幾個 Header 來達成 Cache 的效果。

### Expires
用來定義 Cache 資料的過期時間 t，以此來告訴 Browser 資料在 t 時間後才需要更新資料。

  ![img_expires](https://i.imgur.com/dHlGCR0.png)
  
如上圖，Server 告訴 Client 這個 Response 在 _Thu, 09 Aug 2018 00:00:00 GMT_ 後才過期。而 Client 在這個時間到之前就不會再發出 Request 跟 Server 要資料。

而 **Expires** 有一缺點，其是回傳特定的時間點 **_t_** ，若 Client 有調整過系統時間或是因不同時區造成其時間為 **_t'_** 而 **_t < t'_**，則 Expires 就會失去Cache 的效果，同樣發出 Request 來拿資料 (如下圖)。

![img_expire_issue](https://i.imgur.com/NpNTbcf.png)

### Pragma : no-cache
用來讓 Client 告訴 Proxy 是否使用 Cache。

  ![img_pragma](https://i.imgur.com/NXft5vh.png)
  若有 _no-cache_ ，則 Proxy 會再向來源 Server 發送 Request 取得資料；
  若無 _no-cache_ ，則直接由 Proxy 回覆 Cached 的資料

### Last-Modified / If-Modified-Since
顧名思義，Server 在 Response 回傳特定的時間點在 _Last-Modified_ ，而後續 Client 就將這個時間放在 _If-Modified-Since_ 來告訴 Server，Client 的 Cache 是哪個時間點的資料，來判斷是否要回傳新的資料和時間。

  ![last-if](https://i.imgur.com/I3qZ30E.png)


---
## HTTP 1.1
在 HTTP 1.1 針對 Cache 增加了像是 [Cache-Control](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9), [ETag](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.19)，來完整 Cache 機制

### [ETag](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.19) / [If-None-Match](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.26)

**ETag** 通常會是一段 Server 產生的 hash 字串，例如：_UOqMY6DFJ/mlGYgYDOfJGg==_ ，而這字串就是給 Client 後續驗證資料是否有更動的依據，就像是透過 MD5 驗證檔案有沒有被更改。

**If-None-Match** 則是 Client 收到 Server 的 ETag hash 字串之後，在 Request 用這個 Header 並夾帶 hash 字串，讓 Server 驗證請求的資料是否有變動。

   * 若沒變動，則回傳 [304 Not Modified](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.3.5) 告知 Client，並且可在 Response 中再夾帶 cache-control: Max-Age 讓 Client 重新計算資料的 Timeout 時間。 

   ![304](https://i.imgur.com/hq37xvz.png)

  * 若有變動，則回傳 [200 OK](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.2.1) 和新的資料，並在 Response 中夾帶新的 ETag 和 cache-control: Max-Age。

  ![200](https://i.imgur.com/1yKBifm.png)


---

## Reference
* [RFC 2616 Caching in HTTP](https://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html#sec13)
* [HTTP 快取](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching?hl=zh-tw)
* [循序漸進理解 HTTP Cache 機制](https://blog.techbridge.cc/2017/06/17/cache-introduction/)
* [Cache Control 與 ETag](https://blog.othree.net/log/2012/12/22/cache-control-and-etag/)
* [REST笔记(五):你应该知道的HTTP头------ETag](https://www.cnblogs.com/tyb1222/archive/2011/12/24/2300246.html)
* [What's the difference between Cache-Control: max-age=0 and no-cache?](https://stackoverflow.com/questions/1046966/whats-the-difference-between-cache-control-max-age-0-and-no-cache)
* [初探 HTTP 1.1 Cache 機制](https://blog.toright.com/posts/3414/%E5%88%9D%E6%8E%A2-http-1-1-cache-%E6%A9%9F%E5%88%B6.html)
###### tags: http
