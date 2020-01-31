---
layout: post
title:  "用 Launchbar 快速关闭后台进程"
date:  2017-12-15
author: Minja
---

我装了很多菜单栏工具、后台 Helper，它们不能通过 `⌘Command+⇥Tab`  呼出、关闭，每次都得请活动监视器（Activity Monitor）出场，颇为麻烦。于是写了个 Launchbar 脚本，展示所有后台进程，选中即关闭，还可以多选，挺方便的。

![title](https://raw.githubusercontent.com/BlackwinMin/blackwinmin.github.io/master/lib/2017-12-15-用-Launchbar-快速关闭后台进程/2017-12-15-killall.gif)

这个动作的核心是一段 AppleScript。至于为何用 Launchbar 来调用嘛，当然是爱上这种「下命令」的感觉了。

话说最近 Automator 总算撑不下去，bug 漫天，遂入 Keyboard Maestro、Launchbar 和 Hazel 三大件，一下子跨进了小康。
