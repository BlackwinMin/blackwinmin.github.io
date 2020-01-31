---
layout: post
title:  "LaunchBar 以图搜图"
date:  2018-04-28
author: Minja
---

更新：

1. 支持识别 png、jpg 和 jpeg 等格式；
2. 支持名字带有空格的图片。

---

最近又开始收集图片了。

这是一个不够优雅的以图搜图方案，需要先把图片上传到图床再实现搜索。Action 是用 shell 写的，基本思路是：

1. `curl` 上传图片到 sm.ms 图床；
2. `grep` 提取出返回的图片地址；
3. `sed` 调整为正常网址格式；
4. 调用上一步的变量，拼接出 Google image 所需的网址；
5. `open` 打开 Safari 页面。

![title](2018-04-27-LaunchBar-%E4%BB%A5%E5%9B%BE%E6%90%9C%E5%9B%BE.gif)

[\> 动作下载](https://github.com/BlackwinMin/sspai-sample-script/blob/master/LaunchBar/img%20Search.lbaction.zip)

如有支持直接 POST 图片的搜图 API，还望告知。
