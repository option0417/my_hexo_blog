---
title: Weekly Reading - 2019 May 27 ~ Jun 02
tags: reading
date: 2019-06-04
---

### JWT Related
近來針對專案的登入驗證想做些調整，因此先複習了傳統 Cookie-based 和 Session-based 的驗證方式，也跟著了解何謂 JSON Web Token (JWT)。  

整體來說，JWT 針對 Cookie 和 Session 所遇到的問題 (e.g. CSRF, Distributed Deploy) 都有相對應的解決方案，
但是否就能以 JWT 取代，我想主要還是以應用需求、限制、環境等條件總和考量為佳。
* [JSON Web Token(JWT) 簡介](https://blog.cssuen.tw/json-web-token-jwt-%E7%B0%A1%E4%BB%8B-a5719a1b0a70)
* [浅谈使用Json Web Token和Cookie的利弊](https://chengandpeng.github.io/2016/04/15/jwtvscookie/)
* [以 JSON Web Token 替代傳統 Token](https://medium.com/@leon740727/%E4%BB%A5-json-web-token-%E5%8F%96%E4%BB%A3-session-bae47556dde2)
* [以 JSON Web Token 取代 session](https://medium.com/@leon740727/%E4%BB%A5-json-web-token-%E5%8F%96%E4%BB%A3-session-bae47556dde2)
* [講真，別再使用JWT了](http://zhuanlan.51cto.com/art/201708/548195.htm)
* [JWT介绍和优缺点及适用场景分析](https://www.guonanjun.com/220.html)
