---
title: '[WhatIs]  JWT  (JSON Web Token)'
date: 2019-09-05
tags: 
- dev 
- http
---

## 什麼是 JWT (JSON Web Token) ?

JWT 顧名思義，是一種以 JSON 為「明文」資料格式，以 Token 為主的認證機制。 而在傳輸過程中， JWT 會以密文方式呈現，如下範例：

```
  eyJ0eXAiOiJqd3QiLCJhbGciOiJIUzI1NiJ9.
  eyJ1c2VyaWQiOiJhYmMtMTIzIiwidXNlcm5hbWUiOiJOb25hbWUifQ.
  f9eixg-OO06ZLZGpWcvUcAocAlubFT0uRrBW8HhokoY
```

上面範例以 **.** 隔開可分作三個部分： **Header**, **Payload** 和 **Signature** 。

```
  header.payload.signture
```


首先， **Header** 定義 JWT 所使用的加密演算法以及內容類型。 
例如：

````
    {
      "alg": 加密演算法
      "typ": JSON 資料類型
    }

````

而 **Payload** 則是放業務邏輯相關的資料。
例如：

```
{
  "userid": "abc-123",
  "username": "Wei-De Su",
}
```

接著 **Signture**，就是將上面 Header 和 Payload 的內容經過 [Base64 for URL](https://tools.ietf.org/html/rfc4648#section-5) 的方式轉為密文，再以 **.** 將內容合在一起進行加密演算後產生的密文。

_例如以 HMAC256 作為加密演算法_
```
Signture = HMAC256(Base64(header).Base64(Payload))
         = f9eixg-OO06ZLZGpWcvUcAocAlubFT0uRrBW8HhokoY
```

## 為什麼要用 JWT (JSON Web Token) ?
### 1. 安全性
  * cookie-base 的認證機制會將資訊儲存在 Client 端 (ex. Browser)，但這樣的方式會有 [CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)) 的安全性議題。

### 2. 可擴展性
  * Session-base 的認證機制會將資訊儲存在 Server 端，這樣的方式在分散式架構就會有 Session 在多節點如何同步的問題。

### 3. 應用廣
  * JWT 除了用於登入驗證外，也可用在一次性驗證的服務上，
    例如購物優惠的驗證、註冊確認的驗證等。



## JWT 要怎麼用 (JSON Web Token) ?

下圖是 JWT 的流程圖：

  1. Browser 發送 _username_ 和 _password_ 到 Server 進行登入。
  2. Server 以登入相關資訊和預寫的 **secret** 產生 JWT
  3. Server 回傳 JWT 給 Browser
  4. Browser 後續發出的 Request 都將 JWT 置於 HTTP Request 的 Header
  5. Server 驗證 Browser 送過來的 JWT 是否正確
  6. 若正確，則回覆資料給 Browser
  
  
![jwt_flow](https://auth0.com/learn/wp-content/uploads/2016/01/17.png)
_Source: [Auth0](https://auth0.com/learn/json-web-tokens/)_

## 延伸閱讀
* [RFC 7519 - JSON Web Token (JWT)](https://tools.ietf.org/html/rfc7519)
* [RFC 7518 - JSON Web Algorithms (JWA)](https://tools.ietf.org/html/rfc7518)
* [RFC 7517 - JSON Web Key (JWK)](https://tools.ietf.org/html/rfc7517)
* [RFC 7516 - JSON Web Encryption (JWE)](https://tools.ietf.org/html/rfc7516)
* [RFC 7515 - JSON Web Signature (JWS)](https://tools.ietf.org/html/rfc7515)

* [浅谈使用Json Web Token和Cookie的利弊](https://chengandpeng.github.io/2016/04/15/jwtvscookie/)
* [以 JSON Web Token 替代傳統 Token](https://medium.com/@leon740727/%E4%BB%A5-json-web-token-%E5%8F%96%E4%BB%A3-session-bae47556dde2)
* [以 JSON Web Token 取代 session](https://medium.com/@leon740727/%E4%BB%A5-json-web-token-%E5%8F%96%E4%BB%A3-session-bae47556dde2)
* [講真，別再使用JWT了](http://zhuanlan.51cto.com/art/201708/548195.htm)
* [JSON Web Token(JWT) 簡介](https://blog.cssuen.tw/json-web-token-jwt-%E7%B0%A1%E4%BB%8B-a5719a1b0a70)
* [JWT介绍和优缺点及适用场景分析](https://www.guonanjun.com/220.html)

* [SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language)

* <a href="https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)">CSRF</a>
  * [讓我們來談談 CSRF](https://blog.techbridge.cc/2017/02/25/csrf-introduction)

* <a href="https://en.wikipedia.org/wiki/Session_(computer_science)">Session</a>
  * [Web 技術中的 Session 是什麼？](http://fred-zone.blogspot.com/2014/01/web-session.html)
  * [介紹一篇關於session的好文章,寫的很詳細](http://yken919.pixnet.net/blog/post/45702341-%E4%BB%8B%E7%B4%B9%E4%B8%80%E7%AF%87%E9%97%9C%E6%96%BCsession%E7%9A%84%E5%A5%BD%E6%96%87%E7%AB%A0%2C%E5%AF%AB%E7%9A%84%E5%BE%88%E8%A9%B3%E7%B4%B0)

* [HTTP Cookie](https://en.wikipedia.org/wiki/HTTP_cookie)
