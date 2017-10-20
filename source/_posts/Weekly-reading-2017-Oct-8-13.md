---
title: Weekly reading (2017/Oct 8-13)
date: 2017-10-14
tags: reading
---

## [Airbnb’s 10 Takeaways from Moving to Microservices](https://thenewstack.io/airbnbs-10-takeaways-moving-microservices)

作者為 [Airbnb](https://www.airbnb.com/) 的工程師[Melanie Cubula](https://www.linkedin.com/in/melaniecebula/)，在本文敘述了 Airbnb 遷移至 Microservices 架構的過程以及10點建議。
Airbnb 從2008年至今，服務已經擴展到191國家65000個城市，在今年夏天總計有450萬人在網站上瀏覽訊息。
而要運作這樣的服務，每週部署了3500個mircoservice，每年部署了7.5萬次，一切為900位工程師努力的結果，並持續成長中。

1. Monolith first
 * 先把主要的業務功能照顧好，再來想最佳化。Airbnb也是在發展到有50萬行程式碼後，才發覺需要做microservice。
2. DevOps culture 
 * 要建立 DevOps 文化，但如何建立和誰來建立在各個企業我想都是個問題，就像導入 Agile 一樣，必須要有熱心的關鍵人物或Team，經由高層的授意或權力釋放，整個建立的過程才能順利。 以Airbnb為例，其是由SysOps起頭，來帶領或教導其他部門的工程師一同來學習，一同建立才有這樣的結果！
3. Configuration as Code
 * 目前許多的 [DevOps tools](https://xebialabs.com/periodic-table-of-devops-tools/)  都是為了這個目的。 因為現在的系統架構都太複雜了，已經不是單純人工可以處理。
4. Monitoring and Alerting
5. Continuous Delivery
6. Automate, Automate, Automate
 * 上面三點就是在講，透過自動化來執行整個軟體從開發到發佈的流程，並透過監控來取得feedback來調整優化流程。
7. Your First Service = Bad
 * 不只業務邏輯，還有架構也是可改變的，簡單講就是，此一時非彼一時也。
8. Services Own Their Data 
 * 只要有一定的規範，自己動手一定最有效率！
9. Break Apart the Monolith
 * 一步一腳印的概念！
10. Standardize Service Creation
 * 這點在前期應該不容易，一方面服務可能還不夠多，一方面也呼應第一點。

### _ref:_
* [Micorservice](https://en.wikipedia.org/wiki/Microservices)
