---
title: Apache2.2 + Subversion1.7.0 安裝設定
date: 2011-10-26
tags: dev
---

這兩天再次安裝了Apache和Subversion，以往在這種情況都習慣於網路尋找教學。 今天希望能為自己留下紀錄，省下搜尋的時間，最主要還能為Blog灌灌水!!

#### **必備軟件(大陸腔!?)**

*   [Apache Http Server](http://httpd.apache.org/) ：  
    這次安裝的版本是 2.2.21
*   [_Apache Subversion_](http://subversion.apache.org/) ：  
    因為Apache只釋出原始碼，懶得自己Build的話得另外找[Binary release](http://subversion.apache.org/packages.html)，個人是下載[Win32Svn](http://sourceforge.net/projects/win32svn/)。
*   [_TortoiseSVN_](http://tortoisesvn.net/) ：  
    SVN裝了Server端當然也要裝個Client端來使用，個人喜歡用小烏龜~

#### **安裝方式(一字記之曰 “Next”)**

*   Apache Http Server ：

![apache01.png](./imgs/apache01.png)
按個幾次Next即可安裝成功!!

*   **Apache Subversion ：**

![apache02.png](./imgs/apache02.png)
多按幾次Next即可安裝成功!!

*   **TortoiseSVN ：**

![apache03.png](./imgs/apache03.png)
同樣的，按Next就對了!!

#### **設定步驟(Ctrl + C & Ctrl + V)**

先來設定Apache Http Server ，首先開啟安裝路徑底下的 `conf\httpd.conf`  
接著找出下面這兩行，並把前面的 # 刪掉

<pre name="7abd" id="7abd" class="graf graf--pre graf-after--p">_LoadModule dav_module modules/mod_dav.so_  
_LoadModule dav_fs_module modules/mod_dav_fs.so_</pre>

再來加入下面這兩行來載入SVN用到的Module

<pre name="8ef9" id="8ef9" class="graf graf--pre graf-after--p">LoadModule dav_svn_module modules/mod_dav_svn.so  
_LoadModule authz_svn_module modules/mod_authz_svn.so_</pre>

並把下面這幾個檔案拷貝到Apache安裝路徑底下的 `/modules`

<pre name="aacf" id="aacf" class="graf graf--pre graf-after--p">_mod_dav_svn.so_  
_mod_authz_svn.so_  
_libdb44.dll (檔名最後一個數字會因版本不同而有所改變)  
libeay32.dll  
ssleay32.dll_</pre>

SVN的Module也可用下面方式載入就不用拷貝那幾個檔案了

<pre name="8444" id="8444" class="graf graf--pre graf-after--p">LoadModule dav_svn_module “_<svn安裝路徑>_/bin/mod_dav_svn.so”  
LoadModule authz_svn_module “_<svn安裝路徑>_/bin/mod_authz_svn.so”</pre>

然後，在最底下加入

<pre name="0a32" id="0a32" class="graf graf--pre graf-after--p"><Location /_<SVN網頁路徑>_>  
 DAV svn  
 SVNListParentPath on  
 SVNParentPath _<SVN Repository Root路徑>_  
 AuthType Basic  
 AuthName “Subversion repository”  
 AuthUserFile _<SVN Repository 認證密碼檔路徑>_  
 Require valid-user   
 AuthzSVNAccessFile _<SVN Repository 授權設定檔路徑>_  
 </Location></pre>

最後，要產生認證密碼檔，  
執行Apache Server資料夾底下的 `\bin\htpasswd.exe -c <密碼檔名> <帳號>`  
產生後將檔案搬到 `httpd.conf`所指的位置。

再產生授權設定檔 ，  
新建一個文字檔並搬到 `httpd.conf`所指的位置。  
接著複製以下內容至檔案中，

<pre name="d04f" id="d04f" class="graf graf--pre graf-after--p">[groups]   
developer = option0417  
everyone = *   
[/]   
* =   
[SVN:/]   
[@developer](http://twitter.com/developer "Twitter profile for @developer")=rw</pre>

完成以上步驟後啟動 Apache Server 就大功告成!!!
