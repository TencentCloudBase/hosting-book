# Egret 游戏如何部署到云开发网站托管


云开发静态托管是云开发提供的静态网站托管的能力，静态资源（HTML、CSS、JavaScript、字体等）的分发由腾讯云对象存储 COS 和拥有多个边缘网点的腾讯云 CDN 提供支持.

使用云开发静态托管可以帮助游戏轻松扛过流量洪峰，让业务平稳运行~同时，可以在 Egret 中接入云开发的 SDK，将数据库、函数、存储等环节也迁移至云开发上，让整个业务不再崩盘。

## 初始化项目
首先， 需要使用 Egret Launcher 初始化一个项目，关于 Egret Launcher 的安装就不再介绍。


打开 Egret Launcher ，创建一个新的 Egret 游戏项目

![](https://postimg.aliavv.com/picgo/20200427095616.png)


项目创建完成后， 可以点击 Egret Wing ，对项目进行编辑

![](https://postimg.aliavv.com/picgo/20200427095638.png)


这里，我们不再编辑，直接执行发布
点击发布按钮，进入到发布页面

![](https://postimg.aliavv.com/picgo/20200427095652.png)

选择 HTML5 ，并点击确定，进行发布

![](https://postimg.aliavv.com/picgo/20200427095738.png)

发布完成后，点击打开文件夹，可以看到构建产物

![](https://postimg.aliavv.com/picgo/20200427100005.png)

![](https://postimg.aliavv.com/picgo/20200427100018.png)

接下来，我们只需要将这些构建产物上传到云开发的静态托管上就可以将 Egret 游戏部署到云开发静态网站托管之上。

## 创建云开发环境
在完成了游戏的开发后， 我们来创建云开发环境，用于后续的部署。访问云开发控制台，点击【新建环境】，创建一个新的环境

![](https://postimg.aliavv.com/picgo/20200427100108.png)

在弹出的环境创建页面，输入你要创建的环境名称。此外，这里计费方式需要选择 按量付费。
![](https://postimg.aliavv.com/picgo/20200427100135.png)


设置完成后，点击立即开通， 就可以开通一个新的云开发环境了。

![](https://postimg.aliavv.com/picgo/20200427100345.png)

你会看到你的环境名变成了你输入的字符加一段随机生成的字符串，这个是你的环境 ID，你可以记录一下你的环境 ID ，后续会用到。稍等片刻，云环境初始化完成后，点击进入详情页面，点击左侧的静态网站托管，

![](https://postimg.aliavv.com/picgo/20200427100402.png)

你会进入到静态托管的详情页面，点击开始使用，开通静态托管服务

![](https://postimg.aliavv.com/picgo/20200427100429.png)

等待静态托管服务的开通，稍等片刻，就开通好了。你可以在设置中看到你的域名信息

![](https://postimg.aliavv.com/picgo/20200427100447.png)

比如我的域名是 https://egret-14cdf2.tcloudbaseapp.com/，这个域名是云开发分配给我的测试域名，可以让我在没有迁移到生产环境的时候完成产品的测试。

## 安装云开发 Cli & 登陆

我们可以通过云开发控制台手动上传这些文件，也可以使用云开发 cli 工具上传。

![](https://postimg.aliavv.com/picgo/20200427100522.png)


考虑到我们在工作中绝大多数场景都是使用 Cli 来完成上传的，因此，这里我们将会使用 Cli 来上传。

关于 CLi 工具安装就不在此赘述，大家可以直接去看云开发的官方文档：http://docs.cloudbase.net/cli/intro.html，按照官方文档进行安装即可。

在完成 cli 工具的安装后，执行如下命令来登陆


```
tcb login
```

登陆完成后，可以看到这样的界面。

![](https://postimg.aliavv.com/picgo/20200427100555.png)


## 上传文件
完成了云开发 Cli 的配置，接下来我们可以来上传文件到云开发，使用命令行，进入到我们刚刚生成的项目文件夹中，比如我这里是进入到了   这个目录 ,然后在这个目录中执行命令进行部署

    tcb hosting:deploy -e egret-14cdf2

稍等片刻，我们的文件就上传完成了。

![](https://postimg.aliavv.com/picgo/20200427100629.png)

访问我们刚刚拿到的测试环境的网址，可以看到这样的界面，则说明我们成功的将游戏部署到云开发静态网站托管之上，接下来我们只需要绑定域名，就可以将游戏上线啦~

![](https://postimg.aliavv.com/picgo/20200427100650.png)
