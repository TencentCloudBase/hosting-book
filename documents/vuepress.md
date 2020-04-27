# 如何将 VuePress 部署到云开发静态网站托管

VuePress 是社区广受好评的文档插件，不少的项目都开始使用 VuePress 来构建团队的文档、产品的官网。现在，你也可以在云开发上托管你的 VuePress 文档啦！不需要再忍受中美网络之间的波动导致的网络性能差和速度慢的问题啦！Let's Go

云开发（CloudBase）是一款云端一体化的产品方案 ，采用 serverless 架构，免环境搭建等运维事务 ，支持一云多端，助力快速构建小程序、Web应用、移动应用。
云开发静态网站托管支持通过云开发SDK调用服务端资源如：云函数、云存储、云数据库等，从而将静态网站扩展为全栈网站
无论是腾讯云·云开发用户，还是小程序·云开发用户，只要开通按量付费，即可享有云开发静态网站托管服务。

## 系统依赖
在进行后续的内容前，请先确保你的电脑中安装了 Node.js 运行环境。如果没有安装，可以访问 nodejs.org  下载安装。

## 安装云开发 cli 工具 和 VuePresss
执行如下命令，安装云开发 cli 工具以及 VuePress

    npm i -g @cloudbase/cli vuepress


## 在本地初始化一个 VuePress 项目
首先，在本地创建一个目录，这里以 tcb 为例

    mkdir tcb && cd tcb

进入到 tcb 目录后，创建一个默认的 hello world 文件

    echo "# Hello TCB & Vuepress" > README.md

![](https://postimg.aliavv.com/picgo/20200427114944.png)


然后，执行命令，启动，并查看效果。

    vuepress dev

等待其编译完成，打开浏览器，访问 localhost:8080

![](https://postimg.aliavv.com/picgo/20200427115013.png)

可以看到刚刚创建的文档产生的页面

![](https://postimg.aliavv.com/picgo/20200427115033.png)

这样，就说明我们完成项目的初始化了。

## 创建一个云开发环境

完成了本地的 Vuepress 建设，接下来我们来创建一个云开发环境，用来部署 VuePresss 。打开腾讯云控制台，在产品中找到云开发

![](https://postimg.aliavv.com/picgo/20200427115149.png)

进入到云开发的管理控制台，点击新建环境，新建一个环境来进行部署


![](https://postimg.aliavv.com/picgo/20200427115251.png)


新建一个环境，名为 docs，并选择按量计费，开通环境

![](https://postimg.aliavv.com/picgo/20200427115307.png)

在开通环境以后， 记住你的环境 ID，这个 ID 后续我们会用到。

创建完成后，点击环境，进入到环境的管理页面。点击左侧菜单栏中的「静态网站」

![](https://postimg.aliavv.com/picgo/20200427115337.png)

并在静态网站页面开通功能

![](https://postimg.aliavv.com/picgo/20200427115357.png)

当你看到这样的界面时，就说明已经开通好了。

![](https://postimg.aliavv.com/picgo/20200427115424.png)


你现在可以通过上传文件手动上传一个文件测试，稍后，我们将会用云开发 Cli 来完成上传。

## 初始化云开发 Cli
完成了云开发环境的配置后， 我们需要初始化一下云开发 cli ，从而实现借助 cli 来上传页面（当然， 也可以通过网页端直接上传，但 VuePress 如果文档页面较多，还是使用 Cli 上传更简单）

在命令行输入如下代码

```
tcb login
```

会提醒你需要在网页中授权

![](https://postimg.aliavv.com/picgo/20200427115535.png)


在弹出的页面确认授权

![](https://postimg.aliavv.com/picgo/20200427115548.png)


确认授权后，你会看到控制台输出相应的命令
 
这样，你的云开发 cli 就初始化好了。 接下来，就可以进入到最后一个环节，上传部署 VuePress 了。

## 部署 VuePress
接下来，我们来构建，并部署 VuePress。
回到我们刚刚创建的 VuePress 的目录，执行命令构建静态页面

    vuepress build

构建完成后，会提醒你，生成的静态文件在 .vuepress/dist

![](https://postimg.aliavv.com/picgo/20200427115807.png)

    cd .vuepress/dist

然后执行命令上传文件，记得将这里的 EnvID 替换为你自己的环境的环境 ID。

    tcb hosting:deploy ./ -e EnvID

稍等片刻，文件就上传好了

![](https://postimg.aliavv.com/picgo/20200427120504.png)

此时，你在云开发管理控制台也可以看到这些文件，说明成功上传。

![](https://postimg.aliavv.com/picgo/20200427120519.png)


## 访问

点击设置，进入设置页面，可以找到默认的的域名，点击域名，就可以看到你刚刚部署的环境啦。

![](https://postimg.aliavv.com/picgo/20200427120537.png)


比如，我的部署以后是这样的

![](https://postimg.aliavv.com/picgo/20200427120559.png)

## One More Thing
只需简单的几步，你就可以轻松实现将 VuePress 部署到云开发上，无需再忍受 Github Pages 的龟速啦！还不快迁移？

不仅如此，如果你是一个自动化爱好者， 还可以试着把云开发 Cli 配置到你的 CI 环境中，实现自动部署哦～

