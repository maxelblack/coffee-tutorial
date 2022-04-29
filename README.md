# Coffee Tutorial

这是一个面向新手的 Java 教程，中文译名“咖啡入门指南”。

教程整体使用中文编写，在部分技术名词和专有名词上使用英文以保持与其他资料的通用性。主要面向萌新群体，在基本概念上的解释尽可能通俗易懂，同时排除了一些难懂的概念。

网站: https://coffee.maxelbk.eu.org

Written with ❤ by Maxel Black and other contributors. Powered by [Hexo](https://hexo.io) & [Doku Theme](https://github.com/SukkaW/hexo-theme-doku)

## 在本地使用网页预览

请安装最新的 Node.js 环境（推荐使用 LTS 版本），然后安装 Hexo 命令行工具：

```shell
npm install -g hexo-cli
```

将这个仓库 clone 到本地：

```shell
git clone https://github.com/maxelblack/coffee-tutorial.git
```

然后 `cd coffee-tutorial` 切换到网站源码目录，安装依赖：

```shell
npm install
```

最后开启由 Hexo 提供的临时服务器即可：

```shell
hexo server
```

## 参与教程编写

为保证教程文案的统一性和较大的可理解程度，以及防止自动构建环境爆炸，这里提出一些编写规范。

### 文件和 node 环境

推荐使用 `npm` 管理 node 环境，但请一定使用新版，目前 `package-lock.json` 是 Version 2 ，以后也将会随着 npm 更新而更新，若使用旧版本可能会出现一些奇怪的问题。

包管理也可以使用 `yarn` ，但请不要将相关的配置文件（ `yarn.lock` 之类）提交上来（并不是歧视 yarn ，这样做只是为了保证环境的统一性，实际上 Maxel Black 本人也是在用 yarn 的），类似的 PR 将被无理由拒收。

同样，请不要随意添加和修改绝大多数文件，尤其是 `_config.yml` 和 `_config.doku.yml` 这两个配置文件。一般来说只需要修改 `source` 目录中的文件，若要添加新的侧栏项请在 PR 信息中注明一级和二级侧栏项的名称以及页面的相对地址（这个地址可以参考 `_config.doku.yml` 中现有的地址）。

如有对配置文件内容的改进意见请直接[提Issue](https://github.com/maxelblack/coffee-tutorial/issues/new)。

### 文案规范

#### 页面基本格式

一个页面通常只介绍一个主题，如基本数据类型页面介绍了 Java 中的基本数据类型。

在每一页的顶部可以适当使用默认样式的 `note` 标签（标签用法具体见下方）来写一个前言，比如讲一下“这一页会学到什么”之类的内容，具体参考 主方法内流程 一节的页面顶部内容。

内容应与本页面的主题紧密相关，不能过于离题。有关技术名词和概念应写得尽可能详细和易懂。

同时若页面中使用了有版本区分的工具，应当在页面的顶部使用 `primary` 风格的 `note` 标签注明版本号和生效范围，同时添加 `本页用到的工具版本` 标题。如 JDK 和 Gradle 的使用：

```
{% note primary 本页用到的工具版本 %}
Java Development Kit (JDK) - `11.0.2` // 若无特别说明，在以后的章节里均使用该版本
Gradle - `7.4.2` // 仅本页面
{% endnote %}
```

另外，若中间内容比较多，应使用多级标题分类，并注意页面右侧的目录是否有良好的可读性。标题的具体规范见下方。

#### 空格

在中文与英文之间、文本与插入型代码块之间应添加空格以增强可读性，如下面的文本：

```markdown
Java 标准库提供了一个功能强大的随机数工具，即 `Random` 类。
```

英文和中文标点遇到一起时，应遵循“标点实际占用位置和英文之间一定有空间但尽可能小”的原则。如中文逗号和英文相邻的情况，`Java 通用的 IO 输入流是 InputStream，` 这种写法是错误的，末尾处应写为 `Stream ，`（当然这种情况将 `InputStream` 写到代码块里更加合适）。当然，如果英文在中文逗号后面就不需要加空格，如 `，InputStream` 。

#### 信息提示类内容

请勿将 Markdown 集成的引用语法(即 `>` )用在信息类内容上，使用信息标签 `note` 来代替：

```liquid
{% note [style] [title] %}
Text message.
{% endnote %}
```

其中 `[style]` 是标签的颜色风格，`[title]` 是标签标题，两个属性均可不写。

大多数时候的颜色风格应是蓝色的 `info` ，在有需要的情况下可使用其他风格（如红色的 `danger` 用在严肃的警告内容上等），但注意 `primary` 风格只能用于版本号说明

关于 `note` 标签的更多颜色风格和样例见 [Doku 文档](https://doku.skk.moe/tag-plugins.html) 。

同时请不要滥用信息标签，这种标签主要用来记录一些主题线外的内容或是警告、注意问题等内容，比如在讲构建工具的依赖库管理功能时，用信息标签简单介绍构建工具的其他功能。且**通常**每一个主题中只有两个以内的标签，使用信息标签分类（如分 For Windows / For Linux / For macOS 三种）的情况除外。

除此之外，信息标签还可以用来在教程文本中插入专有名词的介绍，这时请使用 `dark` 风格。例如，在 Gradle 介绍中提到 `shadowJar` 这个工具，可以插入一个 `dark` 类型的标签来简单介绍一下 `shadowJar` 和它的主要功能。

#### 标题

所有的标题都应概括主题并尽可能简短，能用一个字说清楚绝不用两个字。

页面内的多级标题一般应从二级开始，最多到四级。

----

目前的规范就是这些，当出现新的问题时会添加新的规范，请编写者多关注本页的更新。