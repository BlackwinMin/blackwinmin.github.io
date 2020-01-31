![sspai-banner](http://onf0m2glb.bkt.clouddn.com/bitcrom/minja/2017-11-09-133647.jpg)

Title:Workflow 1.7.7 更新：iOS 11 与泛用性
Date:2017-11-09

很长一段时间里我们都觉得 workflow 不会更新了，没想到它 忽然重返公众的视线，增加对新系统与硬件的适配，跟进了 Drag and Drop 操作、HEIF 图片等新特性，在健康与辅助功能方面做出了优化，顺带修了一票旷日持久的 bug，真可谓一次全方位的更新。

在一天的摸索中，我发现这次更新内容虽多，但没有以往动不动就翻天覆地的变化。不过，在制作了健康状况提醒、阅读完 [@顾伶磊](https://sspai.com/user/772807/updates) 先生关于 Voice Over 的微博后，我意识到这次的更新不单单是喂给 Geek 们的兴奋剂，更是一次面向所有人的更新，更易用，更有人文关怀。

我看到了一个成熟的 workflow，一个人人可用的 workflow。

## 更简单的操作：Drag and Drop

Workflow 最大的痛点就是「操作过于繁琐」，是的，它是一个自动化工具，但是过往的 ShareSheet 启动方式步骤过多，我甚至因此把所有文字处理动作搬到了 Copied 上，享受后者 Drag and Drop 拖动的干练。

这次 workflow 最大的改动就是支持 Drag and Drop 添加、移动变量，这让制作、测试乃至运行 workflow 都变得更简单。姗姗来迟，但无愧于我们的等待。

**直接拖拽运行**

![wo](http://onf0m2glb.bkt.clouddn.com/bitcrom/minja/2017-11-09-wo-min.gif)

在 iPad 上，workflow 总算允许通过拖动来输入内容，同时支持文字、链接、图片和文件。例如我想修改一张图片的尺寸，只需要开启分屏，**把图片拖至对应 workflow 顶部的开始按钮上，马上就运行了**。该拖拽功能可在 Split View 和 Slide Over 中使用。回头看看以前，我需要选择图片-分享-run workflow-选择所需 workflow，在升级 iOS 11 后的一段时间里我使用 workflow 的频率因此大大降低，现在我可以迁移回来了。

除了减少操作，Drag and Drop 另一个重要意义在于避免了误触。和我一样拥有大量 workflow 动作的人，在 ShareSheet 弹出菜单里总需要仔细找一找才能瞄准所需动作。

所有的 iPad 用户都可以享受到这直观的操作，而乐于制作 workflow 的 Geek 也有了更方便的测试方式——结合 workflow 和 shelf app：

![架子](http://onf0m2glb.bkt.clouddn.com/bitcrom/minja/2017-11-09-shelf-min.gif)

以往我想测试一个 workflow，只能跳到某个应用里，经由蹩脚的ShareSheet 来测试，来回的跳转、切换工作量不轻。Shelf app 是一类文件暂存工具的俗称，这里以 Yoink 为例，我先把所有想测试的数据从不同应用拖到 Yoink 里，再将 Yoink 全屏、呼出 workflow 悬浮窗，挨个把数据丢进去测试。由于 Drag and Drop 允许同时拖动多个文件，Yoink 又支持文件堆（一次性拖一堆文件），我可以批量进行测试。

这个技巧不单单用于测试，实际使用的时候也很好用。我曾经比喻 shelf app 为搁板，那么现在，workflow 就是在你手边的加工厂。

**拖动变量**

![拖动](http://onf0m2glb.bkt.clouddn.com/bitcrom/minja/2017-11-09-%E6%8B%96%E5%8A%A8%E5%8F%98%E9%87%8F-min.gif)

做简单的 workflow 很轻松，但是长达几十步的 workflow 就另当别论。Workflow 里的魔法变量很灵活，而这次有了更灵活的方式来修改它们：没错，**还是拖动**。长按一个胶囊状的变量，等它「浮」起来，就可以用另一根手指滚动屏幕，把变量拖到需要的地方。

在 iPad 上，这个体验更加出色，我觉得自己在操纵一个控制台，而以前就像是练一指禅。

当然，我认为 Drag and Drop 还有更大的开发空间。理想状态就是拖动变量到 workflow 图标上直接运行而不需要点开、一次性调整多个 workflow 图标位置、批量添加动作。

## 多文件支持

![img](https://cdn.sspai.com/2017/11/09/88cca2b3bfb7e7b3cc44ef274b72f379.png)

Drag and Drop 很棒，但我们不光要拖拽，还要批量处理，多文件支持满足了这个期待。

Workflow 长期以来都可以批量处理图片和链接这些简单内容，可惜对于文件却无能为力，不过这种尴尬已经成为历史了。**Get File 和 Save File 动作均已支持多文件处理**，你可以一次选中多个文件进行处理，或者保存一组文件下来。

目前这两个文件相关动作支持 iCloud、Dropbox 和 Box，我个人的应用场景是把多个 taskpaper 文件（一种任务数据文件）一起导入，转换为 .txt 格式后放进 Mindnode 里生成思维导图。

## 读写更多健康数据

![img](https://cdn.sspai.com/2017/11/09/ab7e11c2b65b8717f14518f88c07e5f4.png)

这次仅次于 Drag and Drop 的更新，当属健康数据的采集了，我视它为从零到一的改变。

这次更新，**Find Health Samples **动作可以从系统的健康应用里搜集不同类型数据——各种食物摄入、各种运动以及其他奇怪的行为——用于后续处理。过去 workflow 读写的健康数据极为有限，我从不关心相关动作，而这次更新当日我就做出了一个 workflow，自动提醒我劳逸结合。

即使不依靠其他三方应用，导入系统所记录的步数、步行距离和睡眠时间就可以做一个简单的精力分析，假设说今天睡得少、动得多，在准备给 TaskPaper（一个任务管理工具）添加任务时 workflow 就会提供 `@dead` 标签（脑力枯竭）的建议，提醒我最好挑一些简单易做的事来干1 。

![img](https://cdn.sspai.com/2017/11/09/15ccd6a4b5f68835c17ef8710e7c9db1.png)

通过 workflow 做数据分析、连接其他应用（我就是用到任务管理上），系统的健康应用可以发挥更大的价值。如果你有一只 Apple Watch，会比我采集到多得多的数据，不妨想想怎么用好它们。控制进食、安排运动都可以，相信自己的想象力。

## 其他适配工作

### 新格式：HEIF 和 HEVC

iOS 11 引入了新的 HEIF 图片格式与 HEVC 编码格式，同等画质、更省空间，workflow 也在其内置的动作中增加了对两种新格式的支持。

Convert image 动作中，你可以选择 HEIF 格式的导出格式，而在 encode video 动作里，则有 HEVC 1920＊1080 和 HEVC 3840＊2160 两种新的编码方式。如果用了保存它们的应用不支持这些格式，它们会自动降为 JPG 的图片和 .h264 的视频。建议在制作动作的时候，先不要使用最新格式，最后导出时再转换成它们。

不过，你需要 iPhone7 以后的机型，我的中古纪手机就不能享受 HEIF 格式。

### iPhone X 屏幕适配

作为苹果的干儿子，workflow 换新发型在意料之中。刘海没有多大的惊喜，不过刚刚拿到新 iPhone 的用户会很开心。

## 重要的 bug 修复

本次修复了大大小小十几个 bug，同样惠及了各类用户。

多数人用户都发现，过去整理 workflow 图标界面时出现的图标变色、名字错位 bug，这可不好受。索性现在一切正常了。

喜欢捣鼓的人，意识到编辑 Text 框时它不会再跑到流程最上面，往 Dictionary 和 List 里添加变量也不会宕机，想在 Widget 使用 Convert image 动作也不再崩溃了。

而身体障碍人士也可以更好地使用 Voice Over 功能。此前 Select Photo 动作的多选功能与 Voice Over 无法兼容，现在，Voice Over 用户也可以多选照片。另外，Voice Over 也总算识别了 Text 框中的 workflow input，用户可以正常做笔记、摘抄等工作了。

另外，习惯使用脸书和推鸟的朋友，恭喜，相关动作又「复活」了。此前因为 iOS 11 取消了内置的社交网络账户，导致一系列动作不可用，现在 workflow 修复了其中两个。你可以在这份[官方说明](https://workflow.is/whatsnew)里查看完整的 bug 修复说明。

## 尾巴

此次 workflow 更新简直是普天同庆，从普通用户到 Power Users 都受益良多。对于爱折腾的人，哪怕一点点的更新，我们都如获珍宝、玩出丰富花样；而更广泛的用户，尤其是关心健康、需要智能设备来辅助生活的人们，可以从中获得切实的便利。

私以为，workflow 被收购后便「不进行功能性更新」的说法是不现实的，如今软硬件、系统与应用高度结合，只要 workflow 还想存活，无论是 workflow 团队（如果他们还存在的话）还是苹果，都必然会让 workflow 对新系统与硬件进行适配。站在苹果的角度，当然希望麾下应用跟进新特性。此外，在 Copied、Pin 等应用的夹击下，虽然仍无人可问鼎强大与简洁兼备的 workflow，但哀其迟迟不更新，操作体验上已经落后于人，在许多细分领域他已然城池失守。此番更新，可以说是必然为之。

从对变量的优化中，我很高兴又看见从前那个 workflow 的 Geek 影子，而开放更多健康数据、修复 Voice Over 的 bug，又透出浓浓苹果味的人文关怀。尽管我们没有看到系统原生版的 workflow，但这次更新已经就未来走向给出了一个答案：

> Simple things should be simple, complex things should be possible.
>
> ——Alan Kay

愿人人有使用好工具的权利。