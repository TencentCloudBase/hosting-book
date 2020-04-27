**简单介绍一下：**

[云开发](https://console.cloud.tencent.com/tcb)：云开发（CloudBase）是一款云端一体化的产品方案 ，采用 serverless 架构，免环境搭建等运维事务 ，支持一云多端，助力快速构建小程序、Web应用、移动应用。

云开发静态网站托管支持通过云开发SDK调用服务端资源如：云函数、云存储、云数据库等，从而将静态网站扩展为全栈网站

[docsify](https://docsify.js.org/)：docsify动态生成文档网站。与GitBook不同，它不生成静态html文件。相反，它聪明地加载和分析您的Markdown文件，并将它们显示为一个网站。要开始使用它，只需创建一个index.html和在静态网站托管页面上部署它.

接下来我们分三步进行：搭建环境→创建项目→部署

**搭建环境**

1.安装Node.js 和 npm

通过 node -v 命令查看本机是否安装，如果没有安装，参考[node.js安装指南 ](https://nodejs.org/zh-cn/download/)根据电脑系统环境进行安装

2.安装cloudbase/cli

```
npm install -g @cloudbase/cli
```

3.安装docsify-cli

```
npm i docsify-cli -g
```

4.测试安装是否成功

```
cloudbase -v
docsify -v
```

如果看到输出版本号，说明已经安装成功。

**创建项目**

初始化这个项目

```
docsify init docs
```

初始化完成后，您可以修改/docs/README.md文件内容，然后在本地运行

![](https://ask.qcloudimg.com/http-save/4744530/5yh4jmxtt3.png)

运行本地服务器

```
docsify serve docs
```

运行成功后，打开浏览器，访问 localhost:3000

![](https://ask.qcloudimg.com/http-save/4744530/dcemg4a3vl.png)

**部署**

创建云开发环境

访问[腾讯云云开发控制台](https://console.cloud.tencent.com/tcb)，新建【按量计费云开发环境】，记住云开发环境ID，我们需要用到云开发网站托管服务，目前只有按量计费的环境才支持静态托管。

![](https://ask.qcloudimg.com/http-save/4744530/cv9czwe7o6.png)  

进入[网站托管控制页](https://console.cloud.tencent.com/tcb/hosting)，开通静态网站托管服务

![](https://ask.qcloudimg.com/http-save/4744530/4zjoq9r78p.png)

当你看到这样的界面时，就说明已经开通好了。

![](https://ask.qcloudimg.com/developer-images/article/4744530/s323at24zr.png)

登入

```
tcb login
```

这个时候会提醒你需要在网页中授权，在弹出的页面确认授权

![](https://ask.qcloudimg.com/developer-images/article/4744530/5u9479pj7j.png)

确认授权后，你会看到控制台输出相应的命令

执行命令上传文件，记得将这里的 EnvID 替换为你自己的环境的环境 ID

```
tcb hosting:deploy ./ -e EnvID
```

稍等片刻，文件就上传好了

![](https://ask.qcloudimg.com/developer-images/article/4744530/kt6b15kb4r.png)

查看静态网站域名和状态

```
 tcb hosting:detail -e envId 
```

这个时候你会看到静态网站域名，打开浏览器访问就可以了

![](https://ask.qcloudimg.com/developer-images/article/4744530/t87kmwkxvw.png)

这个时候你可以访问[云开发控制台](https://console.cloud.tencent.com/tcb/hosting)，查看上传的文件

![](https://ask.qcloudimg.com/developer-images/article/4744530/dol8plx537.png)

 点击设置，就可以看到刚才控制台输出的默认域名，当然你也可以添加自己的域名 

**小结**

部署过程中用到的环境ID envId ，可以在 [云开发控制台](https://console.cloud.tencent.com/tcb) 查看，[docsify](https://docsify.js.org/)的基本使用可以到其官网查看

如果在操作过程中遇到问题，可以评论留下你的问题