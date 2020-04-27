# React 项目如何部署到云开发网站托管
## 导语

React是目前比较火的前端框架之一，除了可以在自有服务器、Github Pages 部署以外，现在你有了一个新的选择，那就是使用云开发静态网站功能来进行部署。

云开发静态网站托管支持通过云开发SDK调用服务端资源如：云函数、云存储、云数据库等，从而将静态网站扩展为全栈网站

云开发（**CloudBase**）是腾讯云为开发者提供的一站式后端云服务，它帮助开发者统一构建和管理资源，免去了移动应用开发过程中繁琐的服务器搭建及运维、域名注册及备案、数据接口实现等繁琐流程，让开发者可以专注于业务逻辑的实现，而无需理解后端逻辑及服务器运维知识，开发门槛更低，效率更高。

**无论是腾讯云·云开发用户，还是小程序·云开发用户，只要开通按量付费，即可享有云开发静态网站托管服务。**

​

## 系统依赖

在进行后续的内容前，请先确保你的电脑中安装了 Node.js 运行环境。如果没有安装，可以访问 nodejs.org  下载安装。

## 安装云开发 **cli** 工具 和 **React**脚手架

在配置好 NodeJs环境后，执行如下命令，安装云开发 cli 工具以及 React脚手架：

​

```
npm install -g @cloudbase/cli
npx create-react-app reactdemo
```


## 本地初始化一个**React**项目

过程中脚手架会自动安装项目中需要的相关依赖，安装完成后可以看到下面这样的输出

​

![](https://postimg.aliavv.com/picgo/20200426175141.png)

安装完成之后进入到项目目录，启动本地预览，成功后项目将会运行在本地的3000端口

​

```
cd reactdemo
yarn start
```


​

![](https://postimg.aliavv.com/picgo/20200426175235.png)


在浏览器中打开localhost:3000，可以看到React的界面，这样说明成功完成了本地开发的项目搭建

​

![](https://postimg.aliavv.com/picgo/20200426175242.png)

## 创建云开发环境

创建一个云开发环境用来部署React项目，可以从微信开发工具创建，也可以通过腾讯云控制台，在产品中找到云开发，这边举例如何从腾讯云中找到云开发

​

![](https://postimg.aliavv.com/picgo/20200426175249.png)


进入到云开发的管理控制台，点击新建环境，或者使用现有的环境来进行部署

​

![](https://postimg.aliavv.com/picgo/20200426175255.png)
​

新建一个环境，或者使用已创建的环境，注意这里计费方式需要选择按量计费，因为只有按量计费才可以进行开通静态网站

​

![](https://postimg.aliavv.com/picgo/20200426175345.png)

​

开通环境后，有一个环境ID，这个ID后续会使用到，点击对应的环境进入环境的管理页面，点击菜单栏中的静态网站，开通静态网站服务

​
![](https://postimg.aliavv.com/picgo/20200426175353.png)
​

出现下面图示的界面，说明已经开通成功了。

​

![](https://postimg.aliavv.com/picgo/20200426175359.png)
​

现在我们通过云开发的CLI来完成React项目的部署。

##  初始化云开发**CLI**

​

完成了云开发环境的配置后，需要登陆云开发 cli ，从而实现借助 cli 来进行部署（当然， 也可以通过网页端直接上传）

在命令行中输入

![](https://postimg.aliavv.com/picgo/20200426175406.png)

将会跳转到云开发控制台页面进行授权，

​

![](https://postimg.aliavv.com/picgo/20200426175415.png)

​

确认授权后出现下图的界面，证明登陆成功了，同时有个小 tips，就是 cloudbase 可以使用简写命令 tcb 

​

![](https://postimg.aliavv.com/picgo/20200426175422.png)


## 打包**React**项目并部署

回到React项目目录中执行yarn build对项目进行打包，React脚手架将会默认将文件打包到build的目录下

​
![](https://postimg.aliavv.com/picgo/20200426175429.png)

打包完成后，进入到build后的目录执行如下命令来进行部署，envID需要替换成自己的envID

```
cloudbase hosting:deploy -e envId
```

部署完成后，就可以进行预览了

​
![](https://postimg.aliavv.com/picgo/20200426175456.png)

## 线上访问

进入对应环境设置页面，可以找到默认的的域名，点击域名，就可以看到你刚刚部署React项目，由于默认域名仅供测试使用，限制下行速度10KB/S。

​
![](https://postimg.aliavv.com/picgo/20200426175501.png)

​

如果需要对外正式提供网站服务，最好绑定已备案的自定义域名。

​
![](https://postimg.aliavv.com/picgo/20200426175507.png)

## 总结

只需简单的几步，你就可以轻松实现将React生成的SPA应用部署到云开发上，不需要去购买服务器来进行部署，也不用去部署在Github上无法忍受的龟速！省去服务器购买的费用，还不赶快行动起来？