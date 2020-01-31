---
layout: post
title:  "Automator 教程：打造 macOS 上最简单的解压工具"
date:  2017-08-26
author: Minja
---

![title](https://raw.githubusercontent.com/BlackwinMin/blackwinmin.github.io/master/lib/2017-08-26-Automator-教程：打造-macOS-上最简单的解压工具/Automator-%E9%A2%98%E5%9B%BE%E8%93%9D.png)

我找到了最理想的解压方案：双击，解压，搞定。

macOS 的自带解压软件是一场灾难，它天真地认为全世界都用同一个格式、同一种编码的压缩方案。如果你下载了一个「文件名太长无法解压」的文件，那问题八成出在薛定谔的 Archive Utility 上。

试过了几乎所有能找到的解压软件，我忽然意识到一个问题：我追求的只是解压那一时的爽快，而不太在意附加的功能。于是我制作了基于 p7zip 的 Automator 小工具，满足了轻量、快速、稳定及安全的需求。

但 Automator 服务自身的一个缺陷令人无法容忍：对于输入对象的识别很笼统，我右键任何文件和文件夹都会跳出「解压」选项——可是谁会想解压一张图片呢？说到底，还是右键菜单这个实现方式不够优雅，为什么要在菜单里摩挲一番再点击「解压」呢？

本文将介绍用 Automator、p7zip 和 unrar 来实现以下效果：

* 双击压缩包，直接解压
* 支持绝大多数压缩格式

##工作思路

把「右键-解压」减少到「双击解压」一步，是个需要「换脑子」的活儿。我不能再用寄人篱下的「服务（services）」，而是转向封装好的「应用程序」。大致的思路就是做一个 Automator 应用，它可以调用命令行解压程序 p7zip 和 unrar（分别能解压 zip 和 rar）；双击压缩包后，会转到对应的 Automator 应用里进行解压。这一系列动作里，只有命令行程序真正做了解压的工作，其他的则负责告诉解压模块目标在哪。

##安装 p7zip 和 unrar

`brew install p7zip`

`brew install unrar`

两个程序各使用以下命令来解压文件：

`7z x [文件名] -o[解压后存放路径]`

`unrar x [文件名] -o[解压后存放路径]`

暂且搁置一边，稍后烹制。

##制作 Automator 程序

打开 Automator，新建一个「应用程序」,调用 p7zip 和 unrar 的两个应用程序大同小异，这里以 p7zip 为例。我希望 Automator 应用能解压文件，就得告诉它两件事：文件在哪，怎么解压。来添加两个步骤：第一步「拷贝至剪贴板」将获得目标文件名，第二步「运行 shell 脚本」则会调用 p7zip 去解压文件：

![title](https://raw.githubusercontent.com/BlackwinMin/blackwinmin.github.io/master/lib/2017-08-26-Automator-教程：打造-macOS-上最简单的解压工具/Automator-uz2-%E5%88%9B%E5%BB%BA%E5%BA%94%E7%94%A8.png)

最关键的就是 shell 里的命令，全靠它调用 p7zip/unrar。为了防止 shell 罢工，声明一下环境变量（和下一条命令之间用「;」隔开）：

`PATH=$PATH:/usr/local/bin/`

再将「传递输入」设为「作为自变量」，并在用「$@ 」代替文件名，以接收来自上一步的文件。后面那一串「-o/Users/Min/Desktop」代表输出的路径，我习惯把文件解压到桌面：

`7z x $@ -o/Users/Min/Desktop`

至此 Automator 程序制作完毕。将它们保存在不碍眼的地方，得到两只扛炮的小机器人，接下来会为你所用。

##添加格式支持

我的目标是：双击即解压。

为此，务必将压缩包的打开方式指定为方才做好的 Automator 应用，并选择「全部更改」。我暂时只指定了两个常见格式，「unzip」应用对应 zip，「unrar」对应 rar。

![title](https://raw.githubusercontent.com/BlackwinMin/blackwinmin.github.io/master/lib/2017-08-26-Automator-教程：打造-macOS-上最简单的解压工具/Automator-uz2-%E8%AE%BE%E5%AE%9A%E6%89%93%E5%BC%80%E6%96%B9%E5%BC%8F.png)

养兵上午，用兵下午，至此我们得到了理想效果：

 ![title](https://raw.githubusercontent.com/BlackwinMin/blackwinmin.github.io/master/lib/2017-08-26-Automator-教程：打造-macOS-上最简单的解压工具/Automator-uz2-%E6%95%88%E6%9E%9C.gif) 

##结语
Mac 的自带解压工具只能用于部分 zip，但它的交互方式是最简单的。命令行软件的交互更加是噩梦，尽管它们有着强大的解压能力。为了让解压这件事更加简单，只好我自己动手，丰衣足食。也许双击解压才是最符合直觉的方案，并且我实现了。

算上上个季度的博文，我前前后后写了三篇文章来记录这一段折腾经历。这是一个很有意思的过程，让我回忆起熬夜做 workflow（iOS）的日子，可惜随着后者被苹果收购，Automator 的项目经理离职，自己做小工具越来越难。以往我们爱调侃使用这些自动化工具是「带着镣铐跳舞」，如今简直就有末日旅游的味道了——真不知道哪天它们就被巨头们彻底抛弃了。

总之，现在，我可以说一句：我发现了 macOS 上最简单的解压方式。
