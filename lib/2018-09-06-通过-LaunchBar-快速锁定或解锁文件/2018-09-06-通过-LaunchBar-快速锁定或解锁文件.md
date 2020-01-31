---
layout: post
title:  "通过 LaunchBar 快速锁定或解锁文件"
date:  2018-09-06
author: Minja
---

简单精致的小工具，总是让人一对眼就喜欢上。最近接触到了 F-Lock，一个快速锁定、解锁 Mac 文件的工具，可以避免文件被误删，真是给我这种「桌面日清」的家伙上了一道保险。

但是玩劲儿过了，就觉得多装一个工具比较麻烦，于是用 LaunchBar 实现了文件的锁定与解锁（注意文件图标上的小锁头）。

![title](2018-09-06-Kapture%202018-09-05%20at%2015.32.00.gif)

[>锁定动作下载 🔗](https://github.com/BlackwinMin/sspai-sample-script/blob/master/LaunchBar/File%20Lock.lbaction.zip)
[>解锁动作下载 🔗](https://github.com/BlackwinMin/sspai-sample-script/blob/master/LaunchBar/File%20Unlock.lbaction.zip)

这组动作用了一段 AppleScript，锁定相关的代码部分没有什么难度，倒是 AppleScript 里**路径的处理**值得注意一下。一般来说，AppleScript 自己（不通过 `do xx script` 召唤其他语言）智能处理 Alias 格式的路径，比如这样：

```
Macintosh HD:Users:apple:Desktop:测试.png
```

而一般自动化工具收到的路径却是常见的 Linux 路径格式，LaunchBar 也不例外：

```
/Users/apple/Desktop/测试.png
```

为了能让 AppleScript 认出它要处理的文件路径，需要加一段代码来实现转换：

```
set newPath to POSIX path of thePath
set newAlias to POSIX file newPath as alias
```

而 LaunchBar 是可以一次处理多个文件和文件夹的，所以可以在上面代码的前后加上循环部分，实现批量处理：

```
repeat with thePath in thePaths
	set newPath to POSIX path of thePath
	set newAlias to POSIX file newPath as alias
	做点啥
end repeat
```

以上。

参考：[AppleScript Programming/Aliases and paths](https://en.wikibooks.org/wiki/AppleScript_Programming/Aliases_and_paths)
