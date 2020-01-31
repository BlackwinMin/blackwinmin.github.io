---
layout: post
title:  "用 LaunchBar 批量修改图片宽度"
date:  2018-07-21
author: Minja
---

平时排文章，常常需要修改图片宽度。电脑自带工具的体验非常糟糕，修改功能似乎是被刻意藏起来一样。所以写了个 LaunchBar 动作，快，还能批量操作。

![title](https://raw.githubusercontent.com/BlackwinMin/blackwinmin.github.io/master/lib/2018-07-21-用-LaunchBar-批量修改图片宽度/2018-07-21-%E4%BF%AE%E6%94%B9%E5%9B%BE%E7%89%87%E5%88%86%E8%BE%A8%E7%8E%87.GIF)

[> 动作下载 🔗](Link)

这个动作用 shell 脚本编写，封装了一段 convert 命令，其中涉及用户输入的部分用到了 AppleScript。完整代码如下：

```
#!/bin/bash
#
# LaunchBar Action Script
#

read -r -d '' applescriptCode1 <<'EOF'
    set imgWidth to text returned of (display dialog "请输入图片宽度" default answer "900")
    return imgWidth
EOF

imgWidth=$(osascript -e "$applescriptCode1")

for ARG in "$@"; do
    PATH=$PATH:/usr/local/bin/
    convert -resize $imgWidth "$ARG" "$ARG"
done
```

你可以修改其中的宽度预设值 `900` 为你最常用的数值，比如常见的题图尺寸 `1440`。
