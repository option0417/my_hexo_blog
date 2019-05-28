---
title: Install VirtualBox on Mac Mojave v10.14.5
tags: note
date: 2019-05-24 19:14:54
---


大約 5 月中更新了 MacOS，又過了幾天，好死不死想整理一下 VM 也順道更新了 Virtual Box，也就碰到了這個 Issue...

根據這篇 [Virtualbox installation fails on macOS Mojave 10.14.5](https://www.reddit.com/r/MacOS/comments/bqbowl/virtualbox_installation_fails_on_macos_mojave/)，這狀況主要跟安裝第三方軟體的驗證有關。

解決的方式就是

1. 重啟 Mac，進入 Recover Mode
2. 開啟 Terminal，輸入 ``` spctl kext-consent add VB5E2TV963 ```
3. 再次重啟 Mac，重新安裝 VirtualBox

目前官方已經正在 [處理](https://www.virtualbox.org/ticket/18645) 這問題，相信後續的版本就會修復。

這件事對我最大的啟示: **沒事別更新，不更新沒事**


## ref:
* [Virtualbox installation fails on macOS Mojave 10.14.5](https://www.reddit.com/r/MacOS/comments/bqbowl/virtualbox_installation_fails_on_macos_mojave/)
* [Install of kernel drivers fails with osx 10.14.5](https://www.virtualbox.org/ticket/18645)

* [Installation fails on 10.13.x, 10.14.x (rc=-1908)](https://forums.virtualbox.org/viewtopic.php?f=8&t=84092&start=75)
