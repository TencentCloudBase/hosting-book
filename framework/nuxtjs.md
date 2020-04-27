
# Nuxt.js 项目如何部署到云开发网站托管


最开始了解到Nuxt是在vue SSR下了解到，用过之后感觉真香。 可以省去路由划分的时间，Nuxt.js 会读取该目录下所有的 .vue 文件并自动生成对应的路由配置、进一步封装Vuex等等。下面来介绍如何将Nuxt部署到静态托管上？ 

云开发（Tencent CloudBase，TCB）}是云端一体化的后端云服务 ，采用 serverless 架构，免去了移动应用构建中繁琐的服务器搭建和运维。同时云开发提供的静态托管、命令行工具（CLI）、Flutter SDK 等能力极大的降低了应用开发的门槛。

环境要求
- node.js

工具准备
- Nuxt脚手架： create-nuxt-app
- 云开发命令工具： @cloudbase/cli

## 安装
安装Nuxt脚手架

    npm i create-nuxt-app

安装云开发命令工具 CLI
    
    npm i -g @cloudbase/cli

> 测试 cloudbase/cli 是否安装成功 可以使用cloudbase或tcb命令



    cloudbase -v

或

    tcb -v

## 创建Nuxt项目
    npx create-nuxt-app demo

## 紧接着进入到项目目录下（这里是demo）

1. 在命令行下执行`npm run generate`生成静态html文件
2. 在项目目录中会生成一个dist文件夹。该文件夹下的文件就是生成的静态文件

![](https://postimg.aliavv.com/picgo/20200426181429.png)


## 将 Nuxt 静态网站托管到云开发

首先我们打开 云开发

![](https://postimg.aliavv.com/picgo/20200426181522.png)


选择或创建自己的云开发环境

![](https://postimg.aliavv.com/picgo/20200426181531.png)

这里要注意选择是按量计费的模式(只有按量计费才能开通静态网站托管)。


![](https://postimg.aliavv.com/picgo/20200426181655.png)

创建成功后会自动对环境进行初始化(此过程大概2~3分钟)。

![](https://postimg.aliavv.com/picgo/20200426181702.png)

初始化成功后我们进到对应的环境中找到静态网站托管并开始使用

![](https://postimg.aliavv.com/picgo/20200426181712.png)

等待静态网站服务初始化后就可以使用啦~

接下来我们就可以将nuxt的静态网站上传到云开发静态网站托管了。

首先执行登录命令

    tcb login

![](https://postimg.aliavv.com/picgo/20200426181849.png)

在弹出的页面进行授权

![](https://postimg.aliavv.com/picgo/20200426181901.png)

接着，将静态网站进行部署到云开发静态网站托管

这里我们将dist文件夹下的所有文件都部署到静态网站托管中，执行命令

    tcb hosting:deploy 文件夹  -e 云环境ID

这里的文件夹是将此文件夹下所有的文件都部署到云开发的根目录中，云环境ID可在环境ID下查看

![](https://postimg.aliavv.com/picgo/20200426181915.png)

因为我们希望将dist下的所有文件部署上去，所以上面的命令我们可以写成

    tcb hosting:deploy ./dist -e demo-1cdbae

![](https://postimg.aliavv.com/picgo/20200426181939.png)

上传成功后我们会发现，静态网站托管中多了许多文件

![](https://postimg.aliavv.com/picgo/20200426181946.png)

那我们如何浏览呢？

云开发默认提供了一个与环境对应的默认域名，可以通过这个默认域名进行访问。

![](https://postimg.aliavv.com/picgo/20200426181954.png)

![](https://postimg.aliavv.com/picgo/20200426181959.png)

这样至此我们的Nuxt就部署成功啦


但默认域名存在限制下行速度10KB/S，如果正式使用的话需要添加一个已经备案的域名

![](https://postimg.aliavv.com/picgo/20200426182011.png)

并为其添加dns解析


![](https://postimg.aliavv.com/picgo/20200426182021.png)

![](https://postimg.aliavv.com/picgo/20200426182026.png)

如果可以ping通这个CNAME就可以进行使用自己的域名进行访问啦~~

