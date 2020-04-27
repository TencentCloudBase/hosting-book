# 如何将 Hugo 博客部署到云开发静态网站托管

**Hugo**是一个用Go编写的静态站点生成器，它具有丰富的主题资源和较好的生成速度。

**云开发（CloudBase）**是一款云端一体化的产品方案 ，采用 serverless 架构，免环境搭建等运维事务 ，支持一云多端，助力快速构建小程序、Web应用、移动应用。

云开发静态网站托管支持通过云开发SDK调用服务端资源如：云函数、云存储、云数据库等，从而将静态网站扩展为全栈网站。

无论是腾讯云·云开发用户，还是小程序·云开发用户，只要开通按量付费，即可享有云开发静态网站托管服务。

# 作者介绍

腾讯云云开发布道师——俞焕。任职于腾讯前端开发工程师，全栈开发者，就职腾讯游戏市场体系TGideas团队，负责开发了多款针对线下的跨端小程序应用，有丰富的云开发实践经验，同时也负责部分中台系统的开发，对Vue.js在构建Web后台系统上有较多的实践经验。

# 安装Hugo

首先，我们先安装hugo：

```javascript
brew install hugo
```

> windows的用户可以去Hugo的githubc仓库上下载安装hugo的可执行程序进行安装，具体安装流程请点击这里。

紧接着，我们用hugo来帮我们创建一个blog项目：

```javascript
hugo new site hugo-demo && cd hugo-demo
```

然后我们先创建一个测试的文章:

```javascript
hugo new posts/my-first-post.md
```

最后，直接在目录中运行：

```javascript
hugo server
```

在浏览器打开 http://localhost:1313/ 即可查看效果:

![](https://postimg.aliavv.com/picgo/20200427110358.png)

当然，我们需要部署的是编译完成的静态页面文件：

```javascript
hugo -D
```

生成好的静态页面文件会放在项目的public目录中，目录结构如下：

```javascript
├── 404.html
├── categories
│   ├── index.html
│   └── index.xml
├── dist
│   ├── css
│   │   └── app.1cb140d8ba31d5b2f1114537dd04802a.css
│   └── js
│       └── app.3fc0f988d21662902933.js
├── images
│   └── gohugo-default-sample-hero-image.jpg
├── index.html
├── index.xml
├── posts
│   ├── index.html
│   ├── index.xml
│   ├── my-first-post
│   │   └── index.html
│   └── page
│       └── 1
│           └── index.html
├── sitemap.xml
└── tags
    ├── index.html
└── index.xml
```

如果你不喜欢hugo站点的默认主题样式的话，可以自行在github上找到开源的hugo主题，并放置到你的hugo项目中，例如：

```javascript
git clone https://github.com/olOwOlo/hugo-theme-even themes/even
```

当然，这篇文章的重点不是教大家如何使用hogu，而且如何在云开发上部署静态的站点。

# 静态托管部署

我们进入腾讯云的云开发(cloudbase)控制台，选择开通一个云环境:

![](https://postimg.aliavv.com/picgo/20200427110420.png)

这里要注意选择是按量计费的模式(只有按量计费才能开通静态网站托管)。创建完成后，点击进入我们刚刚创建的云环境，进入云环境管理界面：

![](https://postimg.aliavv.com/picgo/20200427110426.png)

在云环境管理界面，在右侧的网站托管中，我们可以将刚刚项目中生成好的静态页面给上传上去。当然，手动上传显得不太友好，我们也可以借助 cloudbase cli 以命令行的方式执行上传。

首先，安装cloudbase cli:

```javascript
npm install -g @cloudbase/cli
```

执行登录命令：

```javascript
tcb login
```

![](https://postimg.aliavv.com/picgo/20200427110503.png)

在弹出的页面确认授权:

![](https://postimg.aliavv.com/picgo/20200427110511.png)

接着，在hugo-site中将public目录中的文件给部署上去：

```javascript
cloudbase hosting:deploy ./public  -e EndId
```

这里的 EnvID 替换为刚创建好的环境ID。

![](https://postimg.aliavv.com/picgo/20200427110525.png)

腾讯云云开发的静态网站托管有默认域名可供访问：

![](https://postimg.aliavv.com/picgo/20200427110535.png)

通过默认域名，我们就能访问啦:

![](https://postimg.aliavv.com/picgo/20200427110542.png)


# One More Thing

只需要简单的几步，你就能得到你喜欢的站点样式了，丰富的资源更是能满足多样化的需求，还不快试试？

​

> [云开发（CloudBase）](https://cloudbase.net/)是一款云端一体化的产品方案 ，采用 serverless 架构，免环境搭建等运维事务 ，支持一云多端，助力快速构建小程序、Web应用、移动应用。
> 技术文档：https://www.cloudbase.net/
> [点击此处](https://console.cloud.tencent.com/tcb?from=12304)快速使用云开发
> 微信搜索：腾讯云云开发，获取项目最新进展