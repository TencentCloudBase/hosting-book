# LayaBox Air 游戏如何部署到云开发网站托管

云开发静态托管是云开发提供的静态网站托管的能力，静态资源（HTML、CSS、JavaScript、字体等）的分发由腾讯云对象存储 COS 和拥有多个边缘网点的腾讯云 CDN 提供支持.

使用云开发静态托管可以帮助游戏轻松扛过流量洪峰，让业务平稳运行~同时，可以在 LayaBox 中接入云开发的 SDK，将数据库、函数、存储等环节也迁移至云开发上，让整个业务不再崩盘。

## 初始化项目
打开 Laya Air IDE, 初始化一个项目，这里我们将其命名为 cloudbase,放在桌面上。

![](https://postimg.aliavv.com/picgo/20200427101954.png)


可以点击运行按钮，运行创建好的游戏模板，看一下效果。

![](https://postimg.aliavv.com/picgo/20200427102010.png)


正常运行后，就说明我们配置好了一个项目。

## 发布项目

点击顶部菜单栏的 **发布** 按钮，进入发布流程

![](https://postimg.aliavv.com/picgo/20200427102035.png)


选择发布平台为 Web，并点击发布，等待游戏的自动发布

![](https://postimg.aliavv.com/picgo/20200427102506.png)


发布完成后，会提示你查看发布文件夹

![](https://postimg.aliavv.com/picgo/20200427102521.png)


打开后，可以看到编译完的内容

![](https://postimg.aliavv.com/picgo/20200427102533.png)



这些就是 Layabox 游戏的所有文件了，接下来只要将这些文件上传到云开发的静态存储中，就可以让我们使用 LayaBox 开发的游戏享受到高性能的网站托管了。

## 创建云开发环境

在完成了游戏的开发后， 我们来创建云开发环境，用于后续的部署。访问云开发控制台，点击【新建环境】，创建一个新的环境

![](https://postimg.aliavv.com/picgo/20200427102558.png)


在弹出的环境创建页面，输入你要创建的环境名称。此外，这里计费方式需要选择 按量付费。

![](https://postimg.aliavv.com/picgo/20200427102612.png)


设置完成后，点击立即开通， 就可以开通一个新的云开发环境了。

![](https://postimg.aliavv.com/picgo/20200427102629.png)


你会看到你的环境名变成了你输入的字符加一段随机生成的字符串，这个是你的环境 ID，你可以记录一下你的环境 ID ，后续会用到。稍等片刻，云环境初始化完成后，点击进入详情页面，点击左侧的静态网站托管，

![](https://postimg.aliavv.com/picgo/20200427102643.png)


你会进入到静态托管的详情页面，点击开始使用，开通静态托管服务

![](https://postimg.aliavv.com/picgo/20200427102656.png)


等待静态托管服务的开通，稍等片刻，就开通好了。你可以在设置中看到你的域名信息

![](https://postimg.aliavv.com/picgo/20200427102709.png)


比如我的域名是 https://layabox-15b541.tcloudbaseapp.com/，这个域名是云开发分配给我的测试域名，可以让我在没有迁移到生产环境的时候完成产品的测试。

![](https://postimg.aliavv.com/picgo/20200427102724.png)

## 安装云开发 Cli & 登陆
我们可以通过云开发控制台手动上传这些文件，也可以使用云开发 cli 工具上传。

![](https://postimg.aliavv.com/picgo/20200427102739.png)


考虑到我们在工作中绝大多数场景都是使用 Cli 来完成上传的，因此，这里我们将会使用 Cli 来上传。

关于 CLi 工具安装就不在此赘述，大家可以直接去看云开发的官方文档：http://docs.cloudbase.net/cli/intro.html，按照官方文档进行安装即可。

在完成 cli 工具的安装后，执行如下命令来登陆


    tcb login 


登陆完成后，可以看到这样的界面。

![](https://postimg.aliavv.com/picgo/20200427102822.png)

 
## 上传文件
完成了云开发 Cli 的配置，接下来我们可以来上传文件到云开发，使用命令行，进入到我们刚刚生成的项目文件夹中，比如我这里是进入到了 C:\Users\xxx\Desktop\Cloudbase\release\web  这个目录 ,然后在这个目录中执行命令进行部署

    tcb hosting:deploy -e layabox-15b541


稍等片刻，我们的文件就上传完成了。

![](https://postimg.aliavv.com/picgo/20200427102842.png)


访问我们刚刚拿到的测试环境的网址，可以看到这样的界面，则说明我们成功的将游戏部署到云开发静态网站托管之上，接下来我们只需要绑定域名，就可以将游戏上线啦~

![](https://postimg.aliavv.com/picgo/20200427102852.png)


## 总结

将 Layabox 开发的游戏部署到云开发静态网站托管上十分简单，只需要简单的配置一下云开发 cli ，就可以将 LayaAir IDE 开发出来的项目部署到云开发静态网站托管之上。

在实际使用过程中，因为测试域名有限速的配置，因此，建议大家绑定自己的域名，查看效果。 



