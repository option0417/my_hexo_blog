---
title: Java Static Analysis Tools
date: 2017-11-13
tags: dev
---

程式是人寫的，而人寫的就有可能會有失誤發生，又或是經驗不足，寫出了有[漏洞](https://en.wikipedia.org/wiki/Vulnerability_(computing%29)或 [Bug](https://en.wikipedia.org/wiki/Software_bug) 的程式。這時就所以需要工具來幫我們來做檢查。 又或著要統一整體開發的 [Coding Style](https://developer.mozilla.org/en-US/docs/Mozilla/Developer_guide/Coding_Style)，與其耗費人力檢查，同樣的還是透過工具檢查簡單省力！

這篇就來簡單介紹我之前在案子上常用的三種不同的靜態程式碼分析工具，分別是能檢查 Bug 或漏洞的 _**FindBug**_ 和 _**PMD**_，以及能定義及檢查 Coding Style 的 _**CheckStyle**_

### 1. _[FindBugs](http://findbugs.sourceforge.net/)_
首先是個人覺得最好用的 FindBug，為何好用？因為它能幫我們發現可能產生 bug 的程式，從是否有確實釋放 IO 資源到是否會產生 dead lock 之類的 concurrent 問題，都能有效的作檢查。 另外也有支援常用 IDE 的 plugin

  * Plugin: 
    * _[Findbugs IntelliJ Plugin](https://plugins.jetbrains.com/plugin/3847?pr=idea)_
    * _[Findbugs Eclipse Plugin](http://andrei.gmxhome.de/findbugs/index.html)_
    * _[Findbugs Maven Plugin](http://gleclaire.github.io/findbugs-maven-plugin/usage.html)_
  * [Analyzing on Xcode](https://developer.apple.com/library/content/documentation/ToolsLanguages/Conceptual/Xcode_Overview/AnalyzingYourCode.html)

### 2. _[PMD](https://pmd.github.io/)_
而 PMD 主要則檢查寫程式時可能發生的錯誤，例如：宣告了未使用的變數，又或是邏輯上的漏洞等，比較算是 coding 上 bad pratice 的檢查。

### 3. _[CheckStyle](http://checkstyle.sourceforge.net/)_
最後的 **CheckStyle** 也許不檢查 bug ，但在統一團隊的 coding style 上則是最好用的一個工具。
小的從間隔幾個空格到變數/方法的命名，都能夠自定義規則。

### _ref:_
1. http://blog.codacy.com/2016/03/22/review-java-static-analysis-tools/
2. http://continuousdev.com/2015/08/checkstyle-vs-pmd-vs-findbugs/

