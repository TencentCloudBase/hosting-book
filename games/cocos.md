# Cocos 游戏如何部署到云开发网站托管


随着各个大型App都推出了自己的小游戏平台，游戏也越来越受到开发者的关注。
Cocos Creator是一个完整的游戏开发解决方案，包含了轻量高效的跨平台游戏引擎，以及能让你更快速开发游戏所需要的各种图形界面工具。这篇文章将介绍下，如何将Cocos Creator的游戏代码通过云开发网站静态托管的方式，快速的部署到线上。

> 本文的重点并不是介绍如何用Cocos Creator开发一款小游戏，所以如果没有Cocos Creator的使用或者开发经验的话，建议先查阅Cocos Creator的开发手册。

### Cocos Creator生成游戏的静态访问文件

假定我们现在已经开发好一款Cocos Creator游戏，点击`Cocos Creator -> 项目 -> 构建发布`，你会看到下面的界面：

![](https://postimg.aliavv.com/picgo/20200427095306.png)


点击构建，就会将我们开发好的游戏编译成可供访问的web游戏项目结构:

![](https://postimg.aliavv.com/picgo/20200427095320.png)


> 这里由于我们是需要再web端访问我们的小游戏，所以在`发布平台`的选项中，我们选择`Web Mobile`。

### 静态托管部署

我们进入腾讯云的云开发(cloudbase)控制台，选择开通一个云环境:

![](https://postimg.aliavv.com/picgo/20200427095331.png)


这里要注意选择是按量计费的模式(只有按量计费才能开通静态网站托管)。创建完成后，点击进入我们刚刚创建的云环境，进入云环境管理界面：

![](https://postimg.aliavv.com/picgo/20200427095337.png)


在云环境管理界面，在右侧的网站托管中，我们可以将刚刚项目中生成好的静态页面给上传上去。当然，手动上传显的不太友好，我们也可以借助 [cloudbase cli](https://docs.cloudbase.net/cli/intro.html) 以命令行的方式执行上传。

首先，安装cloudbase cli:

```
npm install -g @cloudbase/cli
```

执行登录命令：

```
tcb login
```
![](https://postimg.aliavv.com/picgo/20200427095348.png)


在弹出的页面确认授权:

![](https://postimg.aliavv.com/picgo/20200427095357.png)


接着，在项目中将编译好的`build/web-mobile`目录中的文件给部署上去：

```
cloudbase hosting:deploy ./build/web-mobile  -e EndId
```

这里的 EnvID 替换为刚创建好的环境ID。

![](https://postimg.aliavv.com/picgo/20200427095402.png)


腾讯云云开发的静态网站托管有默认域名可供访问：

![](https://postimg.aliavv.com/picgo/20200427095408.png)


通过默认域名，我们就能访问啦。

![](https://postimg.aliavv.com/picgo/20200427095413.png)

我们就能访问啦。不过这里需要注意的是，云开发静态托管的默认访问域名限制了访问的下行速度，对于游戏这种静态资源量较大的项目，建议还是自己购买个域名绑定进行访问。