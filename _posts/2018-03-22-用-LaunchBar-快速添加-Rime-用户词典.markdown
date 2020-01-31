---
layout: post
title:  "用 LaunchBar 快速添加 Rime 用户词典"
date:  2018-03-22
author: Minja
---

<font color="grey">本文预计在 2020 年上半年大更新，附带一系列原创 Rime 相关动作。</font>

Update：[捕获新单词的版本](https://github.com/BlackwinMin/sspai-sample-script/blob/master/LaunchBar/Rime%20Dic%20Capture.lbaction)。选中单词，Instant send 到 LaunchBar，通过此动作以 'iOS\tios' 格式添加到用户字典。

经过月余磨合，Rime 的词库又渐渐丰富起来，能够满足日常写作和笔记了。不过 Rime 不能学习英文单词的拼写（或者我没有找到方法），日常我遇到的许多英文专有名词拼写起来很不方便——尤其是大小写字母组合起来的单词，比如 `iOS`。

于是我做了一个 LaunchBar 动作，快速向用户词典中添加新的**专有名词**。

\> [动作下载](https://github.com/BlackwinMin/sspai-sample-script/blob/master/LaunchBar/Rime%20Dic.lbaction)

<font color="grey">这里的视频被吃了</font>

其实 Rime 的用户词典自定义起来很简单，以我所用的微软双拼方案为例，只需把格式为 `iOS\tios`（`\t` 是制表符）的文本添加到 `luna_pinyin.extended.dict.yaml` 文件最后一行，再按下组合键 `⌃Control - ⌥Option - ~` 来使新配置生效。

于是就有如下思路：

1. LaunchBar 接收 `iOS\sios` 格式的字符
2. 切换到 Rime 用户数据目录 `/Users/apple/Library/Rime`
3. 把 `\s` 换成 Rime 规定的分隔符 `\t`
4. 把替换结果追加到 `luna_pinyin.extended.dict.yaml` 文件末行

不过我没有把部署字典这一步也加进去，因为每次部署要个三五秒，会打断工作，我一般在工作结束后统一部署。
