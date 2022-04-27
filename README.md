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

#### 信息提示类内容

请勿将 Markdown 集成的引用语法(即 `>` )用在信息类内容上，使用信息标签 `note` 来代替：

```liquid
{% note [style] [title] %}
Text message.
{% endnote %}
```

其中 `[style]` 是标签的颜色风格，`[title]` 是标签标题，两个属性均可不写。

大多数时候的颜色风格应是蓝色的 `info` ，在有需要的情况下可使用其他风格（如红色的 `danger` 等）。

关于 `note` 标签的更多颜色风格和样例见 [Doku 文档](https://doku.skk.moe/tag-plugins.html) 。

同时请不要滥用信息标签，**通常**每一个主题中只有两个以内的标签，使用信息标签分类（如分 For Windows / For Linux / For macOS 三种）的情况除外。

----

目前的规范就是这些，当出现新的问题时会添加新的规范，请编写者多关注本页的更新。