# Discuz 静态化部署到云开发网站托管

云开发静态托管是云开发提供的静态网站托管的能力，静态资源（HTML、CSS、JavaScript、字体等）的分发由腾讯云对象存储 COS 和拥有多个边缘网点的腾讯云 CDN 提供支持

# 为什么要做静态化发布？

Discuz 因为其强大的性能，在国内被广泛使用。
但是， Discuz 是一套动态系统，动态系统因为允许用户输入，就存在被破解、攻击的可能。对于企业来说，使用Discuz 意味着将自己的网站放置在敌人的枪口之下，因此，进行静态化发布也就势在必得。
此外，静态化的一个好处是服务器的负载会大幅度降低，对于企业来说，可以降低服务器的支付成本。

# 安装测试Discuz
首页，我们需要本地搭建服务器（这里我推荐大家使用 PhpStudy ）
可以到PhpStudy官网：https://www.xp.cn 下载并安装，安装成功后，打开点击一键启动

![](https://postimg.aliavv.com/picgo/20200427121858.png)

然后到码云上下载Discuz https://gitee.com/3dming/DiscuzL/attach_files ，完成后在本地解压

![](https://postimg.aliavv.com/picgo/20200427121921.png)


最后打开PhpStudy，在网站选项下，创建一个网站域名为 discuz.cn 指向刚才解压的文件，注意的是这里文件路径不能包含中文，可以改一下文件名。

![](https://postimg.aliavv.com/picgo/20200427121946.png)

记得在 Hosts 中将 discuz.cn 指向 127.0.0.1

创建成功后我们在浏览器中打开 discuz.cn 这个域名，会显示安装页面

在第3步安装数据库页面下我们填写管理员密码，然后进行下一步，数据库账号和密码默认是root。

![](https://postimg.aliavv.com/picgo/20200427122028.png)

安装成功后，我们就可以看到下面这个页面，然后我们登入账号进入管理中心

![](https://postimg.aliavv.com/picgo/20200427122037.png)

管理端登入成功后我们开始生成HTML页面，用来部署到云开发环境中

![](https://postimg.aliavv.com/picgo/20200427122048.png)

点击门户下面的HTML管理，设置一下HTML的生成

![](https://postimg.aliavv.com/picgo/20200427122118.png)

设置成功后，我们点击生成首页选项，然后点击生成按钮。如果想生成其它HTML，从频道栏目下开始添加和发布文章再生成。

![](https://postimg.aliavv.com/picgo/20200427122130.png)

显示首页生成完成，这个时候就可以点击首页访问了，成功后就可以看到下图

![](https://postimg.aliavv.com/picgo/20200427122158.png)

## 静态化部署

下面使用云开发部署这个首页，其它页面需要生成HTML页面后在部署。
## 部署到云开发静态网站托管
### 创建云开发环境
访问腾讯云云开发控制台，新建【按量计费云开发环境】，记住云开发环境ID，我们需要用到云开发网站托管服务，目前只有按量计费的环境才支持静态托管。

![](https://postimg.aliavv.com/picgo/20200427122213.png)

进入网站托管控制页，开通静态网站托管服务

![](https://postimg.aliavv.com/picgo/20200427122224.png)

当你看到这样的界面时，就说明已经开通好了。
### 安装云开发CLI 工具
    npm install -g @cloudbase/cli
### 登入
    tcb login

这个时候会提醒你需要在网页中授权，在弹出的页面确认授权

![](https://postimg.aliavv.com/picgo/20200427122248.png)

确认授权后，你会看到控制台输出相应的命令
现在开始部署生成的首页HTML，打开终端，进入upload目录
这个我们用代码工具打开 upload文件夹下的index.html，将选中的这一段删掉

![](https://postimg.aliavv.com/picgo/20200427122259.png)

在终端中执行以下命令开始部署，记得将这里的 EnvID 替换为你自己的环境的环境 ID

    tcb hosting:deploy index.html -e EnvID
    tcb hosting:deploy data data  -e EnvID
    tcb hosting:deploy static/image/common/logo.png static/image/common/logo.png  -e EnvID

上面命令是部署我们生成的HTML页面用到的文件夹
### 查看静态网站域名和状态

    tcb hosting:detail -e envId 

这个时候我们打开浏览器访问静态网站域名，就可以看到下面这个效果图了
### 总结
这里只是部署了首页，其它页面需要添加频道栏目、添加文章后在生成HTML，具体操作可以看官方介绍。