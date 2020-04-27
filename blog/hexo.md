# 如何将 Hexo 博客部署到云开发静态网站托管

Hexo 是被大家广泛使用的静态博客系统， 除了在 Github Pages 部署以外，现在你有了一个新的选择，那就是使用云开发静态网站功能来部署啦！
## 系统依赖

在进行后续的内容前，请先确保你的电脑中安装了 Node.js 运行环境。如果没有安装，可以访问 nodejs.org  下载安装。

## 安装云开发 cli 工具 和 Hexo 
执行如下命令，安装云开发 cli 工具以及 Hexo

```
npm install -g @cloudbase/cli hexo-cli
```

在本地初始化一个 Hexo 项目
首先，我们创建一个 Hexo 项目，执行如下命令

```
hexo init
```


可以看到下面这样的输出

![](https://postimg.aliavv.com/picgo/20200427105723.png)

初始化完成后，进入到目录中，并启动预览

```
cd blog
hexo s
```


然后，在浏览器中打开 localhost:4000 ，可以看到 Hexo 的界面，这样就说明我们成功的完成了 Hexo 的本地初始化

![](https://postimg.aliavv.com/picgo/20200427105746.png)

## 创建一个云开发环境
完成了本地的 Hexo 建设，接下来我们来创建一个云开发环境，用来部署 Hexo 。打开腾讯云控制台，在产品中找到云开发

![](https://postimg.aliavv.com/picgo/20200427105757.png)

进入到云开发的管理控制台，点击新建环境，新建一个环境来进行部署

![](https://postimg.aliavv.com/picgo/20200427105805.png)

新建一个环境，名为 docs，并选择按量计费，开通环境

![](https://postimg.aliavv.com/picgo/20200427105819.png)

在开通环境以后， 记住你的环境 ID，这个 ID 后续我们会用到。
创建完成后，点击环境，进入到环境的管理页面。点击左侧菜单栏中的「静态网站」

![](https://postimg.aliavv.com/picgo/20200427105838.png)

并在静态网站页面开通功能

![](https://postimg.aliavv.com/picgo/20200427105846.png)

当你看到这样的界面时，就说明已经开通好了。

![](https://postimg.aliavv.com/picgo/20200427105858.png)

你现在可以通过上传文件手动上传一个文件测试，稍后，我们将会用云开发 Cli 来完成上传。

## 初始化云开发 Cli
完成了云开发环境的配置后， 我们需要初始化一下云开发 cli ，从而实现借助 cli 来上传页面（当然， 也可以通过网页端直接上传，但如果你博客的文章比较多，还是使用 Cli 上传更加方便）
在命令行输入如下代码

```
tcb login
```

会提醒你需要在网页中授权
在弹出的页面确认授权

![](https://postimg.aliavv.com/picgo/20200427105927.png)

确认授权后，你会看到控制台输出相应的命令

这样，你的云开发 cli 就初始化好了。 接下来，就可以进入到最后一个环节，上传部署 Hexo 了。
## 构建 Hexo 并上传
回到你的 Hexo 目录中，执行 Hexo g 来生成文件，Hexo 会默认将文件生成在 Public 目录下。

![](https://postimg.aliavv.com/picgo/20200427105946.png)

文件生成完成后，可以执行如下命令来进行部署（需要将 EnvID 替换为前面你记下的环境ID）

```
cd public
tcb hosting:deploy ./ -e EnvId
```


稍等片刻，部署完成，接下来就可以预览了。

![](https://postimg.aliavv.com/picgo/20200427110102.png)

点击设置，进入设置页面，可以找到默认的的域名，点击域名，就可以看到你刚刚部署的环境啦。

![](https://postimg.aliavv.com/picgo/20200427110115.png)

比如，我的部署以后是这样的
## One More Thing
只需简单的几步，你就可以轻松实现将 Hexo 部署到云开发上，无需再忍受 Github Pages 的龟速啦！还不快迁移？
不仅如此，如果你是一个自动化爱好者， 还可以试着把云开发 Cli 配置到你的 CI 环境中，实现自动部署哦～

点击以下链接快速开始用云开发静态网站托管部署你的站点：https://console.cloud.tencent.com/tcb?from=12304 

云开发（CloudBase）是一款云端一体化的产品方案 ，采用 serverless 架构，免环境搭建等运维事务 ，支持一云多端，助力快速构建小程序、Web应用、移动应用。

技术文档：https://www.cloudbase.net/
微信搜索：腾讯云云开发，获取项目最新进展
