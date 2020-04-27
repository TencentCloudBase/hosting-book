# 如何将 Gitbook 博客部署到云开发静态网站托管

**云开发静态托管**是云开发提供的静态网站托管的能力，静态资源（HTML、CSS、JavaScript、字体等）的分发由腾讯云对象存储 COS 和拥有多个边缘网点的腾讯云 CDN 提供支持

GitBook 是一个开源的电子书生成工具，可以很方便的帮助你生成简洁大方的电子书，当然，云开发现在也已经支持 GitBook 的部署啦～现在你可以在云开发上部署你的电子书啦～

## 系统依赖

在进行后续的内容前，请先确保你的电脑中安装了 Node.js 运行环境。如果没有安装，可以访问 nodejs.org  下载安装。

## 安装云开发 cli 工具 和 Gitbook

执行如下命令，安装云开发 cli 工具以及 Gitbook

```
npm i -g @cloudbase/cli gitbook-cli
```

## 本地初始化一个 gitbook 电子书项目

首先，我们创建一个 gitbook 电子书项目,执行如下命令来创建一个电子书

```
gitbook init book
```

这样，我们就在 book 目录中创建了一个新的电子书。

![](https://postimg.aliavv.com/picgo/20200427113948.png)

可以执行命令预览一下他

```
cd book
gitbook serve
```

![](https://postimg.aliavv.com/picgo/20200427113957.png)

启动成功后， 打开浏览器的 localhost:4000 ，可以看到我们刚刚新建的电子书

![](https://postimg.aliavv.com/picgo/20200427114008.png)

这样，就说明我们完成了项目的初始化操作。

## 创建一个云开发环境

完成了本地的 Gitbook 创建，接下来我们来创建一个云开发环境，用来部署 Gitbook 。打开腾讯云控制台，在产品中找到云开发

![](https://postimg.aliavv.com/picgo/20200427114017.png)

进入到云开发的管理控制台，点击新建环境，新建一个环境来进行部署

![](https://postimg.aliavv.com/picgo/20200427114023.png)

新建一个环境，名为 docs，并选择按量计费，开通环境

![](https://postimg.aliavv.com/picgo/20200427114028.png)

在开通环境以后， 记住你的环境 ID，这个 ID 后续我们会用到。

创建完成后，点击环境，进入到环境的管理页面。点击左侧菜单栏中的「静态网站」

![](https://postimg.aliavv.com/picgo/20200427114035.png)

并在静态网站页面开通功能

![](https://postimg.aliavv.com/picgo/20200427114042.png)

当你看到这样的界面时，就说明已经开通好了。

![](https://postimg.aliavv.com/picgo/20200427114046.png)

你现在可以通过上传文件手动上传一个文件测试，稍后，我们将会用云开发 Cli 来完成上传。

## 初始化云开发 Cli

完成了云开发环境的配置后， 我们需要初始化一下云开发 cli ，从而实现借助 cli 来上传页面（当然， 也可以通过网页端直接上传，但 Gitbook 如果文档页面较多，还是使用 Cli 上传更简单）

在命令行输入如下代码

```
tcb login
```

会提醒你需要在网页中授权

![](https://postimg.aliavv.com/picgo/20200427114054.png)

在弹出的页面确认授权

![](https://postimg.aliavv.com/picgo/20200427114059.png)

确认授权后，你会看到控制台输出相应的命令

## 部署

这样，你的云开发 cli 就初始化好了。 接下来，就可以进入到最后一个环节，上传部署 Gitbook 了。

## 部署 Gitbook

接下来，我们来构建 Gitbook 的 HTML ，来进行部署，Gitbook 默认会将 HTML 生成在 \_book 目录。我们可以将这个目录下的文件进行上传和部署,执行如下命令（记得将 envId 替换为你自己的环境ID）

```
gitbook build
cd _book
tcb hosting:deploy ./ -e envId
```

![](https://postimg.aliavv.com/picgo/20200427114109.png)

## 访问

点击设置，进入设置页面，可以找到默认的的域名，点击域名，就可以看到你刚刚部署的环境啦。

![](https://postimg.aliavv.com/picgo/20200427114114.png)

比如，我的部署以后是这样的

![](https://postimg.aliavv.com/picgo/20200427114119.png)

这样，就说明你的部署完成啦～

## One More Thing

只需简单的几步，你就可以轻松实现将 Gitbook 部署到云开发上，无需再忍受 Github Pages 的龟速啦！还不快迁移？

不仅如此，如果你是一个自动化爱好者， 还可以试着把云开发 Cli 配置到你的 CI 环境中，实现自动部署哦～