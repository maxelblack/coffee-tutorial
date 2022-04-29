---
title: Gradle项目结构
description: 自动化的项目构建和依赖库管理
type: docs
---

# 写在前面

`Gradle`使用的库仓库是在`Maven Central`（服务器在US），换句话说，在中国如果不用代理`Gradle`的下载速度会很慢。你可以选择使用系统级全局代理（或使用虚拟网卡）来强制让其使用代理服务器，或者也可以手动进行配置，方法如下：

打开（不存在则创建）`~/.gradle/gradle.properties`，向其写入：
```properties
systemProp.http.proxyHost=代理地址，如果使用 Qv2ray 这类软件则要按照软件内显示的去填写
systemProp.http.proxyPort=代理端口
systemProp.http.proxyUser=用户名，如果使用 Qv2ray 这类软件则要按照软件内显示的去填写，通常这类软件无需账号密码，直接留空就行
systemProp.http.proxyPassword=密码
systemProp.http.nonProxyHosts=不走代理的ip，csv格式

##### 下面是https设置，和上面的不是完全一样的，因此你都需要配置 #####

systemProp.https.proxyHost=代理地址，如果使用 Qv2ray 这类软件则要按照软件内显示的去填写
systemProp.https.proxyPort=代理端口
systemProp.https.proxyUser=用户名，如果使用 Qv2ray 这类软件则要按照软件内显示的去填写，通常这类软件无需账号密码，直接留空就行
systemProp.https.proxyPassword=密码
systemProp.https.nonProxyHosts=不走代理的ip，csv格式
```

# 新建项目

所有Gradle的项目起点都是执行通过执行，
```
$ gradle init [目录，默认为 ./ ]
```
指令自带一个很直观的CLI，会询问几个问题。


第一个问题是选择一个项目类型，Gradle init将项目分为：`basic` `application` `library` `Gradle plugin` 这四种。`Gradle`本身并没有项目类型一说，这个类型仅仅是四个预设好了的模板方便开发者去使用。我们先从最基本的 `basic`开始，先来熟悉`Gralde`整体概念然后再深入`Gradle`。

第二个问题是编译脚本的语言选择，目前Gradle官方支持`Groovy`（后面简称gv）和`Kotlin`（后面简称kt或kts，kts特指kt脚本）。这个就看自己喜好了，后文教程两种语言都会有示例，如果不确定应该选什么，那么就选 `Groovy`。

最后就是项目名称啦，默认会使用目标文件夹名称。你可以根据喜好和命名规范随便写。

然后你的目录会大概是这个样子：
```
.
├── build.gradle
├── gradle
│   └── wrapper
├── gradlew
├── gradlew.bat
└── settings.gradle
```
*注意：如果你选择的是`Kotlin`，那么你将不会有`build.gradle`取而代之的是`build.gradle.kts`*

对于集成开发环境的新建项目暂时先不讨论和使用，等熟悉了之后再说明和使用。

# 项目结构

通过刚刚的项目创建，我们的目录下多了许多文件，那么这些文件都是什么呢？

`build.gradle`（或者`build.gradle.kts`）：项目的构建脚本，是用于管理整个项目的，你的库就需要在这里进行配置。

`gradle/`：这里存储的是`Gradle Wrapper`和`Gradle`的其他文件，`Wrapper`是用于在多人合作时避免系统`Gradle`版本不同造成的错误。没什么需求尽量不要动这个文件夹。

`gradlew`和`gradlew.bat`：是`Gradle Wrapper`的启动脚本，当你试图使用从他人那里得到的项目时请使用`Gradle Wrapper`而不是`Gradle`

`settings.gradle`：项目的配置文件，用于定义一些项目级设置、变量等，入门一般用不到。


# 源代码

我们所有的源代码都将存储到`src`文件夹，但这个文件夹并不存在，于是我们创建它。一个源代码文件夹里可以有许多子模块，通常我们将源代码放入`main`模块，单元测试放在`test`模块。我们需要创建对应模块名的文件夹。我们现在并不需要单元测试，所以可以不用创建`test`文件夹。最后在`main`中我们需要创建对应语言的文件夹，这是用于语言隔离，比如`java`文件要放在`java`目录下。对于资源文件，不属于源代码则要放入`resources`下。

听起来有些复杂有些绕，我们来看看最终的目录树：

```
├── build.gradle
├── gradle
│   └── wrapper
├── gradlew
├── gradlew.bat
├── settings.gradle
└── src            <--------- 源代码根目录
    ├── main          <------ main 模块
    │   ├── java        <---- 真正的源代码存储路径
    │   └── resources   <---- 资源文件存储路径
    └── test          <------- test 模块
```
