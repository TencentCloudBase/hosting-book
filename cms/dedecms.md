# 织梦 CMS 静态化部署到云开发网站托管

**简单介绍一下：**

[云开发](https://console.cloud.tencent.com/tcb)：云开发（CloudBase）是一款云端一体化的产品方案 ，采用 serverless 架构，免环境搭建等运维事务 ，支持一云多端，助力快速构建小程序、Web应用、移动应用。

云开发静态网站托管支持通过云开发SDK调用服务端资源如：云函数、云存储、云数据库等，从而将静态网站扩展为全栈网站

[织梦CMS](http://www.dedecms.com)：DedeCMS基于PHP+MySQL的技术开发，支持多种服务器平台，从2004年开始发布第一个版本开始，至今已经发布了五个大版本。DedeCMS以简单、健壮、灵活、开源几大特点占领了国内CMS的大部份市场，目前已经有超过35万个站点正在使用DedeCMS或基于DedeCMS核心开发，产品安装量达到95万。

## 为什么要做静态化发布？
织梦 CMS 是一套动态系统，动态系统因为允许用户输入，就存在被破解、攻击的可能。对于企业来说，使用织梦 CMS 意味着将自己的网站放置在敌人的枪口之下，因此，进行静态化发布也就势在必得。

此外，静态化的一个好处是服务器的负载会大幅度降低，对于企业来说，可以降低服务器的支付成本。

**安装织梦CMS**

首先，我们需要本地搭建服务器（这里我推荐大家使用 [PhpStudy](https://www.xp.cn/) ）

可以到PhpStudy官网：https://www.xp.cn 下载并安装，安装成功后，打开点击一键启动

![](https://postimg.aliavv.com/mbp/xpn86.jpg)



然后到织梦CMS官网： http://www.dedecms.com 下载 [DedeCMS V5.7 SP2正式版](http://www.dedecms.com/products/dedecms/downloads/)，在本地解压

![](https://postimg.aliavv.com/mbp/7uymr.jpg)

最后在PhpStudy网站选项下，创建一个网站域名为 dedecms.cn 指向刚才下![载的织梦CMS文件中的uploads目录](https://postimg.aliavv.com/mbp/lv9r3.jpg)

创建成功后我们在浏览器中打开 dedecms.cn 这个域名，会显示安装页面

在参数配置选项下我们填写数据库密码，默认是root，获取初始化数据体验包

![](https://postimg.aliavv.com/mbp/xlhim.jpg)

安装成功后，会显示下面这个页面，这个时候我们点登入网站后台，账号和密码默认都是admin

![](https://postimg.aliavv.com/mbp/wdttt.jpg)

登入成功后，开始生成静态文件，用来部署到云开发静态网站托管上

点击生成选项，在更新主页HTML页面中 点击更新主页HTML按钮

![](https://postimg.aliavv.com/mbp/v0oi6.jpg)

在更新栏目HTML页面中，点击开始生成HTML按钮

![](https://postimg.aliavv.com/mbp/venho.jpg)

在更新文档HTML页面中，我们点击开始生成HTML

![](https://postimg.aliavv.com/mbp/urksn.jpg)

这个时候我们访问主页 http://dedecms.cn/  就可以看到生成的静态HTML页面



**部署到云开发静态网站托管**

创建云开发环境

访问[腾讯云云开发控制台](https://console.cloud.tencent.com/tcb)，新建【按量计费云开发环境】，记住云开发环境ID，我们需要用到云开发网站托管服务，目前只有按量计费的环境才支持静态托管。

![](https://postimg.aliavv.com/mbp/elt64.jpg)

进入[网站托管控制页](https://console.cloud.tencent.com/tcb/hosting)，开通静态网站托管服务

![](https://postimg.aliavv.com/mbp/bfejg.jpg)

当你看到这样的界面时，就说明已经开通好了。

![](https://postimg.aliavv.com/mbp/xk59i.jpg)

登入

tcb login

这个时候会提醒你需要在网页中授权，在弹出的页面确认授权

![](https://postimg.aliavv.com/mbp/l82w1.jpg)

确认授权后，你会看到控制台输出相应的命令



现在部署生成的静态HTML页面，打开终端，进入uploads目录

执行命令上传文件，记得将这里的 EnvID 替换为你自己的环境的环境 ID

```powershell
tcb hosting:deploy ./index.html -e EnvID
tcb hosting:deploy ./a ./a -e EnvID
tcb hosting:deploy ./templets ./templets -e EnvID
tcb hosting:deploy ./images ./images -e EnvID
```

上面命令是部署我们生成的HTML页面用到的文件夹

查看静态网站域名和状态

```powershell
tcb hosting:detail -e envId 
```

![](https://postimg.aliavv.com/mbp/ip2kd.jpg)

这个时候我们打开浏览器访问静态网站域名，就可以看到下面这个效果图了

![](https://postimg.aliavv.com/mbp/br3zm.jpg)

这篇文章到这就结束了，织梦CMS的基本操作建议到他们官网看看。