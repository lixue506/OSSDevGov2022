# 开源期中报告

**项目序号**：39

**项目id**：3959939691

**项目名**：yhatt/marp



**小组成员分工**

刘新新51215903085：项目的基本背景和发展历程介绍

周逸平51215903101：项目的历史轨迹分析

袁梦逸51215903093： 洞察项目被归档的可能原因



## 一、项目的基本背景和发展历程介绍

### 1.1 技术类型

Marp使用增量DOM提高性能，实时预览是Marp的主要功能，但是在大的markdown中遇到了性能问题，该问题是由从头到尾重新创建/重新渲染DOM引起的。于是作者团队通过基于增量DOM（由Google）的差异创建/渲染方法来改进它。在 Marp （markdown-it） 中使用的 markdown 解析器可以输出解析的 AST 对象，最好实现外部渲染器以从 AST 转换为增量 DOM。 增量DOM是一个库，用于构建DOM树并在数据更改时就地更新它们。 它与已建立的虚拟DOM方法的不同之处在于没有创建中间树(现有树是就地修改的)。 这种方法显著减少了DOM树增量更新的内存分配和GC抖动，因此在某些情况下显著提高了性能。增量式DOM主要用于作为模板语言的编译目标。它可以用于实现供人类使用的更高级别的API。API经过精心设计，以最小化堆分配，并在不可避免的地方确保增量GC可以回收尽可能多的对象。 其API的一个独特的特性是,它将打开和关闭的标签,适用于作为模板的编译目标语言允许(暂时)不平衡的HTML模板(如标签中打开和关闭单独的模板)和任意逻辑创建HTML属性。

基于 Markdown-it 创建 Marp渲染器和实现增量DOM, 为了转换为HTML / PDF幻灯片，目前Marp已经强制使用jQuery来呈现markdown-it的结果。作者认为这种方法是不好的，因为它会因为范围太广而产生复杂的代码。所以作者基于markdown-it创建Marp的渲染器。通过这种方式，Markdown语法输出HTML的规范将变得清晰，这意味着能够更轻松地创建测试/主题。 

在Marp中，表示模式是最重要的特性请求，但并没有通过对象之间过于复杂的依赖来实现(主进程/窗口进程/编辑器/预览)。呈现幻灯片的组件化将能够更容易地开发表示模式。开发人员可以关注其在跨平台应用程序中的行为。



### 1.2 版本发布历史

#### 版本0.0.5

#### 版本0.0.6:

**更新**

- 应用全新的图标和加载动态浏览图示

- 支持图像从文件路径的相对路径 （yhatt/mdslide）.md

- 存储窗口大小和最大化状态。（yhatt/mdslide）

- 改进幻灯片中的链接打开行为

- 改进表情符号呈现。

**对于开发人员**

- 更新到电子 1.1.3.

- 改进幻灯片 CSS （ CSS 变量 / 拆分的 MD 预览样式 / 准备页码 ）



#### 版本0.0.7

**更新**

- 支持指令
  - 使用指令显示页码page_number
  - 按全局指令、调整幻灯片大小。\$width \$height \$size

- 将默认幻灯片大小从 A4 更改为 4：3，以便与 PowerPoint 兼容

- 支持按自定义大小导出PDF

- 支持使用D&D快速插入图像

- 支持打开多字节编码文本文件

- 错误修复：无法解析包含多字节的图像路径

- Windows：修复了无法解析被 拆分的图像路径的问题

**对于开发人员**

- 更新到Electron 1.2.1，改进了幻灯片预载荷JS

- 改进幻灯片 CSS（更多CSS变量/ Flexbox 居中）



#### 版本0.0.8

**更新**

- 盖亚主题
  - 按视图更改主题->*主题*
  - 添加指令：`$theme template`

- 支持自定义比例图像：`![ 50% ](...)`

- 支持图像居中：`![center](...)`

- 在编辑器上实现上下文菜单 （yhatt/mdslide）

- 查看菜单的状态存储每个窗口

- 帮助菜单：访问网站和打开示例

- 改进初始化窗口显示为闪烁

- 错误修复：仅使用 Markdown 视图时丢失 PDF 上的内容

- OSX上的错误修复：窗口可以通过捏合或双击缩放

**对于开发人员**

- 更新到Electron 1.2.2， jQuery 3.0.0

- 使用而不是npm start gulp run



#### 版本0.0.9

**更新**

- 新语法
  - **背景图片：**`!\[bg](image.png)`
    - 支持选项：`![bg original] ![bg fit] ![bg *%]`
  - **数学公式呈现：**`$c = \pm\sqrt {a^2 + b^2}$`
    - 支持内联 `()` 和块 `($ $$)`
  - **页脚指令：**`<!-- footer: Footer text -->`
  - **预呈现指令：**`<!-- prerender: true -->`
    - 防止在导出 PDF 时出现问题

- 国际化编辑器/主题
  - 使用系统字体作为默认
  - 添加编辑器字体和大小的配置功能

- 改进表情符号渲染
  - 无需网络访问即可渲染
  - 以高分辨率导出

- 添加到交易编码问题 File > Reopen with encoding

- 将电子更新到1.4.3。
  - 提高从非常大的markdown导出PDF的稳定性

- 修复包含空间并由D&D插入的图像路径
-  修复Gaia主题居中标题与自定义样式

- 改进相对路径支持



#### 版本0.0.10

**错误修复**

- 改进了覆盖到锁定文件时的错误处理

- 修复了将Electron降级到v1.3.8的故障表渲染

**Linux**

- 修复了在关闭确认对话框时选择“不保存”时意外终止的问题

- 修复了在关闭确认对话框时按 Esc 键时选择“取消”的问题

**对于开发人员**

- 已正确修复在打包时使用 package .json 的 Electron 版本 

  

#### 版本0.0.11

Marp 0.0.x已经放弃了维护，但此版本将处理重要的安全问题。

**更新**

- 禁止从内联脚本访问本地资源

- 在导出 PDF 时记住上次使用的文件名

- 允许代码突出显示

- 修复文档上的拼写错误和符号

  

#### 版本0.0.12

此版本将成为预发布版本的最后一个版本，除非报告了重要漏洞。

**更新**

- 升级电子和依赖包

- 清理 HTML 导入以避免嗅探本地资源

- fix（幻灯片）： 将@at根指令添加到 ：root选择器 

- 用于包装yarn



#### 版本0.0.13

目前，我们正在开发下一个 Marp，但 v0.0.13 包含安全更新。

- 禁用外部本地脚本以防止绕过 CVE-2017-2239 补丁



#### 版本0.0.14

- 修复电子漏洞 CVE-2018-15685

- 升级一些依赖包版本



### 1.3 主要贡献者的构成（国家、区域和组织等）

- **Yhatt 259 次提交** 

住在日本的网页开发者，周末维护开源，Marp (Markdown presentation ecosystem)的作者。 

- **will-hart 5提交**

墨尔本一家医疗技术公司的产品经理。



### 1.4 CI/CD的使用 

未使用CI/CD。



### 1.5 其他有价值的信息

Marp桌面应用程序是一个简单的Markdown演示文稿编写器，自2017年以来已经停止了维护(2019年左右又维护了几个安全问题)。今天，Marp团队正专注于Marp Next项目，这是面向未来的全新演示生态系统。

为了在各种情况下可用，作者团队构建的全新的Marp Next由多个模块组成。它们是使用JavaScript和TypeScript开发的，并且比以前的Marp更易于维护。Marp Next有两个核心组件：Marpit框架和Marp Core。Marp生态系统的工具通常基于这些。 

Marpit是用于从Markdown创建HTML幻灯片的精简框架。它的设计是将Markdown转换为只有静态HTML和CSS组成的最小资产，输出可以通过Chrome / Chromium打印转换为PDF幻灯片。Marpit是为使用而创建的，作为Marp生态系统的基础，但它也是一个独立的框架。用户可以将Marpit的Markdown转换与您的工具集成，即使它不是Marp：reveal.js、WebSlides等。

Marp Core是一个基础转换器，该项目从Marpit扩展。Marpit只有基本的功能，所以它可能不足以开始编写你的平台。Marp Core提供了实用的语法、附加功能和内置主题。许多功能都是基于旧的桌面应用程序，并经过改进以适合于Marpit。当然，作者团队添加了新的功能来创建更漂亮的平台。模块化的Marp Core为一些工具带来了Marp集成，Marp可以使用Visual Studio Code！

Marp Next有许多应用，例如Marp CLI（Marpit 和 Marp Core 转换器的 CLI 接口）和Marp Web（Marp演示文稿编写器的Web界面）。



## 二、项目的历史轨迹分析

1. 每月新增Star和Fork的个数

   ![image-20220515144149013](https://raw.githubusercontent.com/dcxr969/OSSDev2022/main/img/202205151442207.png)

2. 每月打开Issue和关闭Issue的个数

![image-20220515144657977](https://raw.githubusercontent.com/dcxr969/OSSDev2022/main/img/202205151449638.png)

3. 每月打开PR和合入PR的个数

![image-20220515144754761](https://raw.githubusercontent.com/dcxr969/OSSDev2022/main/img/202205152124715.png)

4. 每月在仓库中活跃（只要有日志产生就算）的不同开发者总数

![image-20220515144946920](https://raw.githubusercontent.com/dcxr969/OSSDev2022/main/img/202205151449244.png)

5. Issue从打开到关闭的平均时长和中位数（单位：天）

![image-20220515145013457](https://raw.githubusercontent.com/dcxr969/OSSDev2022/main/img/202205151450907.png)

6. PR从打开到合入的平均时长和中位数（单位：天）

![image-20220515145052258](https://raw.githubusercontent.com/dcxr969/OSSDev2022/main/img/202205151450295.png)

7. Issue和PR从打开到第一次有人回复（非本人回复）的平均时长和中位数（单位：天）

​	![image-20220515145128478](https://raw.githubusercontent.com/dcxr969/OSSDev2022/main/img/202205151451637.png)

8. 根据你观察到的仓库的历史数据，尝试找到几个你认为关键或值得注意的时间节点

- 2016年5月：该项目被创建

- 2016年7月：该月在仓库中活跃的不同开发者总数达到项目历史上的最高峰，远高于其他月份；此外该月新增Star和Fork的个数、打开和合入PR的个数也是项目历史最高

- 2016年9月：在继2016年7月的开发者活跃盛世之后，出现的一个活跃度小低谷，打开和关闭Issue的个数、打开和合入PR的个数相比附近月份的数据要少许多

- 2018年10月：出现了一个关闭issue的小高峰，但合入PR的个数却为0

- 2019年2月：出现了一个在仓库中活跃的不同开发者总数的小高峰，同时也是新增Star和Fork的个数的小高峰

- 2019年9月：该项目被归档，大量issue被关闭



## 三、洞察项目被归档的可能原因

### 3.1 阅读分析项目的相关信息

#### 3.1.1主页、主要贡献者发表的相关技术博客

- 主页 https://github.com/yhatt/marp
- 相关技术博客 
  - https://marp.app/
  - https://yhatt.github.io/marp/
  - https://marp.app/blog/the-story-of-marp-next

从主页和主要贡献者发表的相关技术博客中可以得知，Marp桌面应用程序自2017年开始停止维护，Marp团队迁移到Marp Next项目，Marp Next项目可以看作Marp项目的升级。

对于Marp的归档原因，主要贡献者表示，他们收到了一份针对过时的Marp应用程序的严重安全报告。通过打开恶意的Markdown文件，攻击者可以远程执行任意代码。出于保护用户免受恶意攻击的责任，Marp项目被归档，并迁移到了Marp Next项目。



#### 3.1.2 Issue 和 PR 中的相关讨论

- https://github.com/yhatt/marp/issues/259

  2018年12月13日，用户创建了issue#259，表示在使用v 0.0.14的Marp时存在XSS漏洞，恶意的script代码会被执行。

- https://github.com/yhatt/marp/issues/267

  2019年2月17日，开发者创建了issue#267，表示Marp在大约3年前就停止了维护，并转而开发Marp Next项目。

- https://github.com/yhatt/marp/issues/276

  2019年9月13日，用户创建了issue#276，表示可以让Marp执行想要的任何代码，这是一个严重的安全漏洞。

- https://github.com/yhatt/marp/issues/277

  2019年9月14日，开发者创建了issue#277，表示停止发布Marp以保护用户免受恶意攻击，Marp for VS Code可以用作Marp应用程序的替代品。



#### 3.1.3 README 文件，贡献者指南，Code of Conduct及其他可能有的相关文档

- README文件 https://github.com/yhatt/marp/blob/master/README.md
- https://github.com/marp-team/marp/blob/main/website/blog/the-story-of-marp-next.md

从Marp项目的README文件和它的升级版Marp Next项目的介绍中，可以得知Marp开发缺乏可维护性，对旧的Marp项目的requests无法得到满足，因此对Marp项目进行了重写升级得到Marp Next项目，升级后的Marp Next项目比Marp项目更易于维护。



### 3.2 项目可能的归档原因

该项目的可维护性不足。Marp不断收到有关过时应用程序的严重安全报告。通过打开恶意的 Markdown，攻击者可以通过远程执行任意代码。作者认为有责任将用户从这些恶意中拯救出来，Marp必须不断发展，以提供最佳的演示平台编写环境，所以将Marp升级成了MarpNext，旧的Marp不再维护。



### 3.3 项目归档后可能产生的影响

#### 3.3.1 对开发者的影响

开发者基于Marp项目，对其进行重构并升级得到Marp Next。在Marp Next中，开发者默认阻止了基于DOM的XSS，这是Marp项目的一重大安全问题。因此，Marp的归档对于开发者来说既是Marp项目的终点，也是新项目的起点，开发者不再对项目继续进行微小的更新和增加额外的功能，也不需要再对issues进行回复，而是在Marp Next项目中进行了重构。

#### 3.3.2 对用户的影响

从用户的角度来说，已归档的Marp项目在其介绍中有明确的引导性文字，用户可以轻易找到升级后的Marp Next项目进行使用，相较于Marp项目，用户在Marp Next项目可以获得更好的使用体验感。



### 3.4 对开源项目如何可持续发展的理解

经过对Marp项目的分析，总结开源项目为实现可持续发展，需要重点关注的问题如下：

1. 经济资源

免费的开源项目大幅降低了开发者的开发成本，但在开源产品使用者对开源产品的贡献和支持方面相对比较缺乏，从而限制了开源软件的进一步价值实现，让开源贡献者成为用爱发电。针对这一问题，GitHub推出了开发者赞助项目GitHub Sponsors，GitHub账号使用者可以以每月定期支付的方式赞助GitHub开发者，Marp Next项目即有此功能。

2. 人力资源

开源项目的可持续发展需要社区开发者可以及时对项目中存在的各种问题进行修改，解答用户在使用过程中遇到的问题，因此开源社区的维护者和贡献者也是开源社区能否可持续发展的重要因素。

3. 开源项目漏洞

Apace Strust2、log4j等漏洞事件应引起社区开发者和开源项目使用者的注意。随着数字产业的蓬勃发展，软件供应链也越发复杂多元，开源产品使用者应精确绘制开源组件依赖链条，以防出现安全漏洞随着开源组件依赖链条逐层传播的问题，从而导致安全危害的不断升级。对于开源项目开发者来说，开源安全风险防范措施应贯穿软件开发的整个生命周期。