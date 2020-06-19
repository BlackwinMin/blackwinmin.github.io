---
layout: post
title:  "用 Shortcuts 将 Kindle 书摘批量导入 Evernote"
date:  2020-06-19
author: Minja
---

喜欢读书的人，往往也乐于做书摘；有了一定数量的书摘后，就需要妥善管理它们。

Kindle[^本文的 Kindle 均指 Kindle 硬件，非 Kindle App] 是不少人阅读的重要平台，其用户有一些现成的书摘管理工具可选择。不过，专门整一个书摘管理工具，一方面会把书摘从整个笔记体系中割裂出去，整理、检索起来都要单独花力气；另一方面，这些管理工具往往比较小众，能存活多久还是未知数，把书摘全权托付给它们，就像是借了别人家的书柜寄存自己的东西，安全感不强。

书摘管理的第一步就是选一个好容器。Hum 表扬过 Evernote 的「容器」属性，它几乎支持任何平台、随处都是收集的入口，格式也没什么限制[^Evernote 的笔记内容为 ENML 格式，基于 HTML 拓展而成，可兼容的内容特别广]。何况书摘不过是一些文本，免费版 Evernote 的空间也够宽敞，这都让人很难拒绝把书摘放进 Evernote。

有了容器之后，就是怎样把大象装进冰箱的问题。此前我在 macOS 上写脚本解决 Kindle 书摘导入问题，而在 iOS 13 之后，iPad 开始支持直连各种 USB 设备，这让我看到了一种新可能：借助 Shortcut，直接把 Kindle 中书摘导入 Evernote！

![title](https://raw.githubusercontent.com/BlackwinMin/blackwinmin.github.io/master/lib/2020-06-19-Shortcut2Kindle/%E5%B0%86%20Kindle%20%E4%B9%A6%E6%91%98%E5%80%92%E5%AF%BC%E5%85%A5%20Evernote.png)

Shortcut 内置了 Evernote 模块，Kindle 的书摘又存储在一份 txt 文档中，这些现有条件让整个方案实现起来不曲折。

[\> 动作下载 🔗](https://www.icloud.com/shortcuts/75eb55f556cf461186a4ec8f16be36da)

<font color="grey">注意：本动作仅支持 iOS 13 系统，如需在旧系统上使用，请根据文章的原理解析部分自行制作。使用前请自行登录 Evernote 或印象笔记帐号进行授权，并在最后一步中填写用于储存书摘的笔记位置。</font>

## 动作使用

导入流程是在 Files 和 Shortcut 中完成的。iOS 13 之后的 Files 可以直接读取 USB 设备中的内容，Shortcut 则负责解析 Kindle 书摘文件、调整格式并导入 Evernote。整个过程借助 Evernote 的 API 在云端完成，与是否安装了 Evernote 应用无关，免费用户也不必担心占用授权设备数量。

下载动作后首次运行时，Shortcut 就会要求你为此动作授权。iOS 13 之后的 Shortcut 动作管理较为严格，每个动作都有独立的权限设置，即便你之前已经在 Shortcut 里登录过 Evernote，现在也需要重新授权。授权后你可以根据 Evernote 模块的指示选择书摘存储位置，不填的话会在默认文件夹中新建一个 Kindle 书摘笔记。

之后将 Kindle 连上 iPad（需要 micro-USB 转 USB-C 转接头），稍等即可在 Files 中看到 Kindle 的文件夹，其中的 My Clippings.txt 文档便是 Kindle 书摘的容身之所。通过分屏模式打开 Shortcut（使用分享菜单也可以，但是分屏模式下的拖曳操作更加直观），将 My Clippings 文档拖到刚才下载的动作上，Shortcut 就会开始解析其中的书摘；之后还会有一个手动筛选的小环节，因为到 Kindle 经常将手抖误划的文本也记录下来，我就设计了这个小步骤供你删掉无用内容。随后，等待书摘上传到云端即可，不一会儿就能在 Evernote 中看到新增的摘抄。

![title](https://raw.githubusercontent.com/BlackwinMin/blackwinmin.github.io/master/lib/2020-06-19-Shortcut2Kindle/%E7%94%A8%E5%BF%AB%E6%8D%B7%E6%8C%87%E4%BB%A4%E7%94%9F%E6%88%90%E5%B8%A6%E6%A0%B7%E5%BC%8F%E7%9A%84%E4%B9%A6%E6%91%98.GIF)

相信你已经注意到，导入后的书摘具有一定的样式，而非干巴巴的纯文本，本文后续也会介绍自定义此类样式的方法。

理论上，本文动作也适用于 iPhone，但是需要借助 Lightning 转接线，我缺乏硬件条件故不能测试。另外，有些读者也许已经用其他管理工具收集过书摘，本文的可以将新增书摘追加到原书摘后面（动作默认是 Append 追加模式），与原有的数据和谐共处。

## 原理简析

在解析 Shortcut 动作之前，我们先从数据的源头开始，检查一下 My Clippings 文档的特点。这一文档中的书摘样式有一定规律，每条都由书名作者、页码、日期和书摘内容组成，像下面这样：

```
真名实姓 ([美]弗诺·文奇)
- 您在位置 #297-298的标注 | 添加于 2019年8月21日星期三 上午11:58:32

密码朋克运动的一个基本信条是，技术解决方案比行政或立法解决方案更可取。
```

每条书摘之前都有一行等于号 `==========` 隔开，在 Shortcut 动作中这些等号可以作为分隔的锚点；而最后 Evernote 中的书摘，则是利用书摘中的书名作者、日期和正文三部分。My Clippings 中书名、日期和摘抄内容与 Evernote 成品笔记之间的对应关系如下图：

![title](https://raw.githubusercontent.com/BlackwinMin/blackwinmin.github.io/master/lib/2020-06-19-Shortcut2Kindle/%E6%8F%90%E5%8F%96%E4%B9%A6%E5%90%8D%E3%80%81%E6%97%B6%E9%97%B4%E5%92%8C%E6%91%98%E6%8A%84%E5%86%85%E5%AE%B9.png)

之所以能够从一段纯文本变成富有风格的摘抄，是因为我用了一段 HTML 模板，将 My Clippings 中的数据拆分后填充了进去。样式转换的关键步骤，归结成一句话就是「套模板」；而 Shortcut 在书摘生成过程中，所负责的事情就是文本提取和模板套用。

### 先从单条书摘开始

生成单条书摘相对简单，其中没有兜圈子的逻辑，适合据此来了解书摘数据提取和 HTML 模板的使用方式。单条书摘的理想效果如下，My Clippings 中的每一「块」数据都会能够被转换成 Evernote 中带样式的笔记：

![title](https://raw.githubusercontent.com/BlackwinMin/blackwinmin.github.io/master/lib/2020-06-19-Shortcut2Kindle/%E6%AF%8F%E6%9C%AC%E4%B9%A6%E7%9A%84%E6%91%98%E6%8A%84%E9%83%BD%E6%9C%89%E6%A0%87%E9%A2%98%E5%92%8C%E6%97%A5%E6%9C%9F.png)

要让 My Clippings 里的数据按「块」转换成书摘，第一步就是借用 My Clippings 自带的 `==========` 分隔线，将其中的数据拆成一块一块；这里有个小细节，My Clippings 最后一行通常也是 `==========`，所以据此拆分后的产物会在末尾捎带上一行空行，可以通过划定文本范围为「从开始到倒数第二」，从而避开最后没有内容的空行。

![title](https://raw.githubusercontent.com/BlackwinMin/blackwinmin.github.io/master/lib/2020-06-19-Shortcut2Kindle/%E6%8E%92%E9%99%A4%E6%9C%80%E5%90%8E%E7%9A%84%E7%A9%BA%E8%A1%8C.png)

有过上面的预加工后，就可以从每一块数据中提取书摘信息。稍加分析 My Clippings 文件中的文本样式，就会发现它们都是高度格式化的，在每两条 `==========` 划分出的文本块中，第一行即书名和作者，第二行包含了摘抄日期，最后一行则是摘抄的具体内容，我们所需的所有信息都准备妥当。

获取标题是最简单的，刚才我们已经发现各条信息是按「行」排列的，所以这次也可以沿用拆分文本的思路，只不过分隔符从 `==========` 变成了换行符。拆开文本犹如庖丁解牛，接下来的事情很方便，一般来说第一行即是标题；偶有第一行是空行的情形，也只需要加一个简单的 IF 判断，在这种情况下转而撷取第二行。不费多大力气，我们就得到了标题。

![title](https://raw.githubusercontent.com/BlackwinMin/blackwinmin.github.io/master/lib/2020-06-19-Shortcut2Kindle/%E8%8E%B7%E5%8F%96%E6%A0%87%E9%A2%98.png)

获取标题时所用的「拆分」思路，也可以推广到其他数据的提取中。摘抄内容的获取如出一辙，只是从第一行改为获取最后一行；而日期的提取要多走一步，借用正则表达式 `20\d\d年.*\d` 过滤出 `20XX年几点几分` 这部分日期时间信息，以省去此前 `您在位置……` 那一长串冗杂信息。

![title](https://raw.githubusercontent.com/BlackwinMin/blackwinmin.github.io/master/lib/2020-06-19-Shortcut2Kindle/%E8%8E%B7%E5%8F%96%E6%91%98%E6%8A%84%E5%92%8C%E6%97%A5%E6%9C%9F.png)

至此，书名 `noteTitle`、日期时间 `noteDate` 和摘抄正文 `noteContent` 三大部分内容都准备妥当，可以进入 HTML 模板套用环节。这一步着实没有技术门槛，即便不太熟悉 HTML 的读者也可以照着葫芦画瓢，将变量名填入即可。

```html
<p><strong>noteTitle</strong></p>
<blockquote style="margin: 1em; padding: 0px 1em; border-left-style: solid; border-left-color: rgb(255, 126, 121);">
		<div style="margin-top: 1em;margin-bottom: 1em;-en-paragraph:true;">
			<span style="color: rgb(136, 136, 136);">
				noteContent
			</span>
		</div>
	</blockquote>
<p style="margin-top: 1em;margin-bottom: 1em;-en-paragraph:true;" align="right">noteDate</p>
```

以上就是单条笔记的摘抄流程。注意，部分 Kindle 书摘管理工具会修改 My Clippings 文件中的文本格式，可能影响正常的摘抄内容（例如下图中就有多余的 `######Knotes######` 文本）。建议检查 My Clippings 文件后再运行快捷指令动作。

![title](https://raw.githubusercontent.com/BlackwinMin/blackwinmin.github.io/master/lib/2020-06-19-Shortcut2Kindle/%E4%BD%BF%E7%94%A8%E8%BF%87%E5%85%B6%E5%AF%BC%E5%87%BA%E5%B7%A5%E5%85%B7%E5%8F%AF%E8%83%BD%E4%BC%9A%E6%94%B9%E5%8F%98%E5%89%AA%E8%97%8F%E6%96%87%E4%BB%B6%E7%9A%84%E7%BB%93%E6%9E%84.png)

### 让书摘按来源书籍归类

我们在同一本书中往往会画出不少句子，如果停留在目前的摘抄模式，则每一句摘抄都会配上书名，看完一本大部头后你可能会在 Evernote 里看到十几条甚至几十条重复的书名，实在没有必要。接下来的优化方向，就是让同一本书的摘抄汇集在同一个书籍标题下，避免重复出现书名。

![title](https://raw.githubusercontent.com/BlackwinMin/blackwinmin.github.io/master/lib/2020-06-19-Shortcut2Kindle/%E5%90%8C%E4%B8%80%E6%9C%AC%E4%B9%A6%E7%9A%84%E6%91%98%E6%8A%84%E5%8F%AA%E9%9C%80%E8%A6%81%E4%B8%80%E4%B8%AA%E6%A0%87%E9%A2%98.png)

例如下图所示《牛津通识读本》的摘抄，就会汇集到 `牛津通识读本：数学(中文版)(蒂莫西.高尔斯)` 的标题之下，不至于出现多次同一标题。

标题去重的基本思路还是**拆分处理**，每次生成一条新摘抄，就把旧的所有摘抄拆开，一条一条检查过去是否存在重复标题。经过模板套用的文本已经没有了 `==========` 分割线，需要另外寻找分隔的锚点；略微观察一下前文的 HTML 模板，可以发现，每条摘抄的 HTML 模板都是 `<p><strong>` 打头的，这些可以作为拆分 HTML 的依据。拆开后，拿每一此获取的标题和现有摘抄比对，分情况处理：

- 如果没有重复，和之前一样，将整个「标题+书摘+日期时间」进模板。
- 如果发现重复，就地将书摘和日期时间信息添加到所属标题下方，不再重复添加标题信息。

![title](https://raw.githubusercontent.com/BlackwinMin/blackwinmin.github.io/master/lib/2020-06-19-Shortcut2Kindle/%E5%8E%BB%E9%87%8D%E6%AD%A5%E9%AA%A4.png)

当前的 Shortcut 动作可以对于 My Clippings 中的数据进行标题去重处理，但是不能直接将 Evernote 已有的旧笔记也进行去重，不是做不到，而是处理太慢。我在 Evernote 中存了百来本书的摘抄，已经让 Shortcut 不堪遍历处理的重负，更喜欢的读书的读者想必压力更大。

这带来的小遗憾就是，如果你过于勤快、读上几章就导入一次，反而会减弱标题去重的效果：尽管每一次导入的书摘都经过了去重处理，但 Evernote 的笔记库里还是可能有重复。一般来说，每周或者半个月导入一次是比较适合的，或者干脆读完几本书后统一导入，总之尽量避开边读边导入的做法。

附：整个 Shortcut 的完整步骤

![title](https://raw.githubusercontent.com/BlackwinMin/blackwinmin.github.io/master/lib/2020-06-19-Shortcut2Kindle/%E5%AE%8C%E6%95%B4%E6%B5%81%E7%A8%8B.png)
