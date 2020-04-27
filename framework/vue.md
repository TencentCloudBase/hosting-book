# Vue.js 项目如何部署到云开发网站托管
**云开发静态托管**是云开发提供的静态网站托管的能力，静态资源（HTML、CSS、JavaScript、字体等）的分发由腾讯云对象存储 COS 和拥有多个边缘网点的腾讯云 CDN 提供支持

在云开发静态托管中，你同样可以托管一个 Vue.js 项目，接下来，我就介绍一下应该如何将一个 Vue.js 项目部署到云开发静态网站托管服务中。

## 初始化一个 Vue 项目

首先，我们使用 Vue cli 创建一个项目，来作为演示。同时，为了符合我们的日常使用场景，引入 Vue Router 组件，并配置 Router 为 Histroy 模式。

```
vue create cloudbase
cd cloudbase
vue add router
```

![](https://postimg.aliavv.com/picgo/20200426174647.png)

执行完成后，可以执行 `npm run serve` 启动预览，查看一下效果

![](https://postimg.aliavv.com/picgo/20200426174701.png)

看完效果以后，可以执行 `npm run build` 来构建出最终的产出物

![](https://postimg.aliavv.com/picgo/20200426174709.png)

可以看到，我们的最终产出物被构建在了 _dist_ 目录中，后续我们只要上传这个目录就好了。

## 创建云开发环境

完成了Vue 项目的创建后，接下来创建云开发的环境,访问[云开发控制台](https://console.cloud.tencent.com/tcb/env/index),点击上方的新建环境，创建一个新的环境。在弹出的界面中输入你的环境名称，并选择**按量计费**，点击下方的**立即开通**，就可以开通一个云开发环境了。

![](https://postimg.aliavv.com/picgo/20200426174717.png)

等待环境初始化完成后，点击刚刚创建好的环境，进入到详情页，点击左侧的环境设置，可以看到环境的 ID， 记住这里的环境 ID，后续上传文件的时候会用到。

![](https://postimg.aliavv.com/picgo/20200426174729.png)

再次选择左侧列表的「静态网站托管」

![](https://postimg.aliavv.com/picgo/20200426174737.png)

在静态网站托管页面选择立即开通。

![](https://postimg.aliavv.com/picgo/20200426174745.png)

等待静态网站托管服务开通后，你就可以看到这样的界面。点击上方的「设置」，可以看到你的测试域名，后续上传后，你就可以在这个测试域名中查看你的站点。

![](https://postimg.aliavv.com/picgo/20200426174753.png)

## 初始化云开发 Cli

完成了环境的创建后，接下来配置云开发 Cli。

### 安装云开发 Cli 并登陆

首先，我们执行命令安装云开发 Cli

```
npm i -g @cloudbase/cli
```

![](https://postimg.aliavv.com/picgo/20200426174804.png)

安装完成后， 执行命令登陆 Cli

```
tcb login
```

系统会自动打开浏览器，你只需要在弹出的页面中登陆你的腾讯云账号，并授予 Cli 权限就可以操作了。

## 上传文件

完成了 Cli 的登陆后，接下来就可以上传文件了。首先，进入到 vue 项目的 dist 目录: `cd dist`，然后，执行命令来上传文件

```
tcb hosting:deploy -e envId
```

这里你需要将 envId 替换为你自己的环境 ID，比如我的替换为 **website-126ca8**，结果如下

![](https://postimg.aliavv.com/picgo/20200426174815.png)

可以看到，我成功的上传了文件，这个时候，我可以直接访问我的测试域名来查看我刚刚上传的 Vue.js 项目。

当你看到这样的界面时，就说明你配置成功了。

![](https://postimg.aliavv.com/picgo/20200426174824.png)

## 一些配置

在 Vue 中，我们常常会用到 Vue Router 的 History Mode 来做更好的 URL，但如果你不做任何配置，在云开发的 Hosting 上就会导致访问时出现 404 错误

![](https://postimg.aliavv.com/picgo/20200426174832.png)

这个问题可以通过在云开发静态网站托管的设置页面将索引文档和错误文档均设置为 index.html 即可。

![](https://postimg.aliavv.com/picgo/20200426174841.png)

## 总结

云开发的静态托管中想要上传 Vue 项目也十分简单，你只需要初始化一个 Vue 项目，并使用云开发的 CLi 工具就可以完成文件的上传。此外，还可以通过修改索引文档和错误文档来实现 Vue Router 的 History Mode 的支持。