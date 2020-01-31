---
layout: post
title:  "快速向 TaskPaper 添加任务"
date:  2018-01-07
author: Minja
---

做了一下 JXA（JavaScript for Automation，Mac 原生 JavaScript）和普通 JavaScript 的功课，最后搞出了 LaunchBar 版的 TaskPaper 任务添加动作。Automator 版也有，而且能实现在弹出框里选择项目，LaunchBar 版的我再研究研究。

![title](https://raw.githubusercontent.com/BlackwinMin/blackwinmin.github.io/master/lib/2018-01-07-快速向-TaskPaper-添加任务/2018-01-07-new-heheeh.gif)

![title](https://raw.githubusercontent.com/BlackwinMin/blackwinmin.github.io/master/lib/2018-01-07-快速向-TaskPaper-添加任务/2018-01-07-new-new_task_via_automator.gif)

如果你想搞 LaunchBar 的动作，注意一个坑：它直接跑 .js 格式的 JavaScript 脚本时用的自己解释器，如果想用 JXA，请把 JavaScript 保存为 .scpt 格式再让 LaunchBar 把它当成 AppleScript 去执行。

简直是狸猫换太子嘛……
