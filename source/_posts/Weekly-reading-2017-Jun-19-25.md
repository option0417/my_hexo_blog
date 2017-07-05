---
title: Weekly reading (2017/Jun 19-25)
date: 2017-06-26
tags: reading
---

## [Where should I put _script_ tags in HTML markup?](https://stackoverflow.com/questions/436411/where-should-i-put-script-tags-in-html-markup)
  最近再次回歸 _Javascript_ 的懷抱，因此才有機會來研究一下為何 _**script**_ 的宣告要放在 Body的最後一行，也就是</body>的上面，
  文章中有解釋這其實關係到 browser 解析 HTML 跟 Javascript 的方式，且在 HTML5 也提供了 **async** 和 **defer** 來處理這個問題。
  掰惹未，目前處於只會用[vanilla.js](http://vanilla-js.com)的狀態，有需要再來找套framework來用吧！

## [Double-precision floating-point format](https://en.wikipedia.org/wiki/Double-precision_floating-point_format)
  如上述，最近在進行 _Javascript_ 的開發，因會需要儲存 _時間戳記 (Timestamp)_ 這樣的資料欄位，也才想到 js 中對於數字的設計和定義是怎樣的，如 Java 和 C 會有 int, long, double 這樣的差異。 而原來 js 中對數字一律定義為 double-precision floating-point，也就是 Double 的概念！

## [An Empirical Study of Load Balancing Algorithms](http://liblb.com/study.html)
  基本上是介紹一個以 Go 寫成的 Load Balance service，但主要作者對於所用的演算法 _Round Robin_、 _Two Random Choices_、 _Consistent Hashing_ 、 _Bounded Consistent Hashing_有著不錯的優劣分析，以及比較。總之，就是乾貨！
