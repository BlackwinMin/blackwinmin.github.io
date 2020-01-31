---
layout: post
title:  "自动清除 Kindle 里无用的 sdr 文件"
date:  2018-06-28
author: Minja
---

虽然给亚马逊缴足了税，我还是更喜欢手动管理 Kindle 里的电子书。既然如此，对于其中的 sdr 索引文件就没法视而不见了。

![title](2018-06-28-%E6%B8%85%E9%99%A4%20Kindle%20%E4%B8%AD%E7%9A%84%20sdr%20%E6%96%87%E4%BB%B6.GIF)

Kindle 会为每一本电子书创建 sdr 索引，但是当你把书删除或归还后，这些索引文件仍然残留。尽管现在的 Kindle 软硬件相较 PaperWhite 时代都有提升，不像当年那样非清理不可，但我仍然坚持「无用的东西就要清理掉」。

思路是这样的：

1. 对于 Kindle/documents 下的每一个文件，先检测是不是 sdr 文件；
2. 对于是 sdr 文件的，寻找同一文件夹中有没有同名电子书；
3. 对于没有同名书籍的，删除。

不巧最近升级了 macOS Mojave 测试版，LaunchBar 挂了，所以只能委屈一下放上 Hazel 版的代码。

```
cd /Volumes/Kindle/documents

mobi=$(echo "$1" | sed 's/sdr/mobi/g')
txt=$(echo "$1" | sed 's/sdr/txt/g')
pdf=$(echo "$1" | sed 's/sdr/pdf/g')
kfx=$(echo "$1" | sed 's/sdr/kfx/g')
azw=$(echo "$1" | sed 's/sdr/azw3/g')

if [[ "$1" =~ "sdr" ]] && [[ ! -e "$mobi" ]] && [[ ! -e "$txt" ]] && [[ ! -e "$pdf" ]] && [[ ! -e "$kfx" ]] && [[ ! -e "$azw3" ]]; then
		rm -rf "$1"
fi
```

这段代码可以修改后放进 LaunchBar 或者 Keyboard Maestro 来手动启用，也可以交给 Hazel，每次拷电子书进 Kindle 的时候（或其他有文件变动的场合）就能自动清理。

目前我遇到的电子书只有 mobi、azw3、txt、pdf 和 kfx 这几个格式，如果你还知道其他 Kindle 能支持的格式，也不妨留言告诉我。
