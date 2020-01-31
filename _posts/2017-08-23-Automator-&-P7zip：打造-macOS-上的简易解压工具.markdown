---
layout: post
title:  "Automator & P7zip：打造 macOS 上的简易解压工具"
date:  2017-08-23
author: Minja
---

![title](https://raw.githubusercontent.com/BlackwinMin/blackwinmin.github.io/master/lib/2017-08-23-Automator-![title](-P7zip：打造-macOS-上的简易解压工具/Automator-%E9%A2%98%E5%9B%BE%E7%BB%BF.png)

作为一个有动手能力的 Mac 用户，如果你不想用破解软件，又找不到合适的解压应用，这篇文章就是为你准备的。
Mac 自带的解压工具 Archive Utility 实在糟糕透顶：支持格式极少、大文件易报错、反复在 zip 和 cpgz 间循环解压，不是一个理想的工具：

![title](https://raw.githubusercontent.com/BlackwinMin/blackwinmin.github.io/master/lib/2017-08-23-Automator-![title](-P7zip：打造-macOS-上的简易解压工具/Automator-uz-%E5%BE%AA%E7%8E%AF%E8%A7%A3%E5%8E%8B.gif)

每次看着压缩包子子孙孙无穷尽，我都感叹：二胎政策真厉害。

Mac 上一直缺乏完美解压方案——也许你从某些奇怪站点下载的「绿色版」BetterZip 例外。我一直想要一款这样的解压应用：

* 速度快、体积小、内存占用少
* 无广告、免费
* 最好开源

在 windows 平台，免费开源的 7z 是不少有识之士的首选。不幸的是 macOS 上只有它的命令行版本，这一截门槛阻碍了许多有心尝试的用户。好在我们有 Automator，可以在右键菜单中打造一个简易解压服务，解决一些基础需求。

##安装 Homebrew

你当然可以直接下载安装 p7zip，但当你贪便宜装了一百个免费命令行程序以后——就知道我们这些写教程的——祥林嫂般强调包管理，是多么必要了。

用这条命令安装它：

`/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

##安装 p7zip
直接用 homebrew 安装 p7zip：

`brew install p7zip`

跑完后看一下 p7zip 的命令，很丰富，从分解压包内单个文件、卷解压/压缩，到设置压缩率，一应俱全。但我们的目的不是成为压缩包达人，而是解决日常所需。

##制作 Automator services
在终端内，我需要运行这样的命令来解压文件:

`7z x [文件名] [存放路径]`

Automator 可以跑 shell 命令，但如你所见，把上面那句话复制粘贴是不会发生奇迹的。需要向它转递正确的[文件名]变量。

打开 Automator 后新建一个 services，它将被用于右键菜单.

首先将输入对象限制为「文件或文件夹」，以防止在不需要解压的 时候蹦出来「解压」选项；添加一个「拷贝至剪贴板」步骤，获得右键所选中文件的名称：

![title](https://raw.githubusercontent.com/BlackwinMin/blackwinmin.github.io/master/lib/2017-08-23-Automator-![title](-P7zip：打造-macOS-上的简易解压工具/Automator-uz-7z%E6%9C%8D%E5%8A%A1.png)

下一步添加「运行 shell 脚本」，将「传递输入」设为「作为自变量」，再用「$@ 」（你不用知道这是什么）来接收上一步获得的文件名。我喜欢把文件解压到桌面，所以添加了「-o」选项，后面直接指定输出路径为桌面：

`7z x $@ -o/Users/Min/Desktop`

考虑到一般我们在用系统默认的 shell，它莫名其妙不会调用你安装的命令，所以需要在上一条命令前声明环境变量。说人话就是，大声告诉它：我叫你一声，你敢应吗！

`PATH=$PATH:/usr/local/bin/`

记得两条命令之间用「;」隔开。

保存好你的造物，运行它试试：

![title](https://raw.githubusercontent.com/BlackwinMin/blackwinmin.github.io/master/lib/2017-08-23-Automator-![title](-P7zip：打造-macOS-上的简易解压工具/Automator-uz-%E6%95%88%E6%9E%9C.gif)

看起来不错嘛。

##局限与对策
除动手的时间成本和一点点技术门槛外，这个解决方案还是和商业软件有着差距：

* 不能直接解压带密码的文件
* 不能方便地单独解压出某一项
* 没有图形界面

即便如此，在多数情况下，它仍是一个不错的解压方案，没有密码的压缩包基本可以成功解压。遇到密码、分卷等复杂情况，也能打开终端应对。没有图形界面在我看来倒是一大优点，你只需要右键目标文件，直接选择「解压」即可，不必「打开应用-选择文件-解压文件-关闭应用」。值得一提的是，在速度上，基于 p7zip 的办法也是虎父无犬子。

另有一个痛点，常见的 rar 作为一种专利格式，是不能用 p7zip 打开的。推荐用免费的 unrar 如法炮制一个右键菜单服务，以实现其解压。

使用自制的小工具让我舒服许多，偶尔遇到不能直接解压的，打开终端也能对付过去。当然，口碑不错的解压应用还有很多，但都不比 p7zip 全能，前者们总是遇到无法解释的格式不支持问题（例如大名鼎鼎的 Unarchiver，就把我的 sketchup 工程解构成了豆腐渣）。

以上。
