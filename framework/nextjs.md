# Next.js 项目如何部署到云开发网站托管
我们知道部署web应用程序的最佳方式是作为静态HTML应用程序，因为他对搜索引擎很友好，速度快等等，这对我们写个人博客这样的小型网站无异于非常nice。如果你的应用可以作为静态HTML，那么可以试试Next.js。

它可以把一个应用程序作为静态页面导出，那么导出的静态页面怎么部署到静态托管呢？我们以云开发静态托管服务为例。

## 什么是云开发？

可以理解为它为我们提前做好了很多的事(例如负载均衡，冷备热备，网络安全等等)，使我们只需关注业务逻辑即可。就像包饺子一样，提前有人给你准备好饺子馅和发好的面，我们只需要包饺子就可以了。详细了解可以到云开发查看

首先我们需要准备的环境以及工具如下：

必要环境:

> node.js
> 开通云环境

开发工具：

> create-next-app
> @cloudbase/cli


下面我们来详细操作~

首先我们进行安装create-next-app

`npm i create-next-app`

以及云开发工具@cloudbase/cli

`npm i @cloudbase/cli`

npm命令是在安装node.js时自动安装


## 构建Next项目
利用脚手架创建一个项目

```
npx create-next-app 项目名称
```

此处项目名称为你的项目根目录名称

创建完成后我们进入到项目中

```
cd 项目名称
```

我们需要在跟目录中新建一个next.config.js文件

```
module.exports = {
    exportTrailingSlash: true,
    exportPathMap: function () {
         return {
            '/': {page: '/'}
         };
     },
};
```

如果你希望生成的静态文件不只包含首页和404页面(Next自动生成),那么可以在next.config.js中加入`'/about': {page: '/about/about'}`,并在pages下新建一个about文件夹并创建about.js文件写入，如果只是测试生成首页和404就够了，那么直接跳到第4步即可

```
const about = () => (
  <div>about</div>
)
export default about
```

附上next.config.js添加后的完整代码：


```
module.exports = {
     exportTrailingSlash: true,
     exportPathMap: function () {
        return { 
            '/': {page: '/'},
            '/about': {page: '/about/about'}
        };
     },
};
```
在package中加入一个script命令
```
"export": "next export"
```
我们运行下列代码来生成静态文件

```
npm run build
npm run export
```

我们发现根目录中生成了一个out文件夹，该文件夹下的所有文件就是我们生成的静态文件，所以接下来要做的事就是开通云环境并将其部署到静态网站托管。

![](https://postimg.aliavv.com/picgo/20200426180817.png)

## 开通云环境
我们打开云开发并创建一个新的环境

![](https://postimg.aliavv.com/picgo/20200426180833.png)

这里要注意选择是按量计费的模式(只有按量计费才能开通静态网站托管)。

![](https://postimg.aliavv.com/picgo/20200426180843.png)

创建成功后会自动对环境进行初始化(此过程大概2~3分钟)。

![](https://postimg.aliavv.com/picgo/20200426180852.png)

初始化成功后我们进到对应的环境中找到静态网站托管并开始使用

![](https://postimg.aliavv.com/picgo/20200426180859.png)

等待静态网站服务初始化后就可以使用啦~


## 部署上传
首先在项目根目录下执行云开发登录命令

```
tcb login
```

![](https://postimg.aliavv.com/picgo/20200426180923.png)


在弹出的页面进行授权操作

![](https://postimg.aliavv.com/picgo/20200426180933.png)

进行上传操作，这里我们希望out文件夹下所有的文件一并上传，所以，我们执行命令
```
tcb hosting:deploy ./out -e 你的云开发环境ID
```
![](https://postimg.aliavv.com/picgo/20200426180948.png)

云环境ID可在环境ID下查看

![](https://postimg.aliavv.com/picgo/20200426180957.png)

上传完成后我们在静态网站托管中可以看到我们out目录下的所有文件

![](https://postimg.aliavv.com/picgo/20200426181009.png)

云开发默认提供了一个与环境对应的默认域名，可以通过这个默认域名进行访问。

![](https://postimg.aliavv.com/picgo/20200426181022.png)

![](https://postimg.aliavv.com/picgo/20200426181026.png)

## 总结
我们总结一下步骤，大体上只有三步

1. 创建Next项目并生成静态文件
2. 开通云环境与静态网站托管服务
3. 使用云开发工具cloudbase/cli命令进行部署上传