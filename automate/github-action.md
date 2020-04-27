## 如何借助 Github Action 将项目部署到云开发静态网站托管

云开发静态托管是云开发提供的静态网站托管的能力，静态资源（HTML、CSS、JavaScript、字体等）的分发由腾讯云对象存储 COS 和拥有多个边缘网点的腾讯云 CDN 提供支持

Github 为开源项目提供了用于静态页面展示的 Pages 服务，很多开发者都在上面托管了自己的静态网站和博客，不少开源项目的案例和文档页面也采用了这种方式。不过由于 Pages 的 CDN 节点大部分在国外，在国内的访问速度不是很理想，不少开发者希望能提升网站在国内的访问速度和稳定性，今天会介绍如何配合 Github Action 的持续集成服务和 云开发 Github Action 扩展，自动部署到访问速度更快的云开发静态托管服务。

![](https://postimg.aliavv.com/picgo/20200427104955.png)

## 云开发静态托管介绍

云开发静态托管是云开发提供的静态网站托管的能力，静态资源（HTML、CSS、JavaScript、字体等）的分发由腾讯云对象存储 COS 和拥有多个边缘网点的腾讯云 CDN 提供支持。可以通过腾讯云控制台、命令行工具以及下面会提到的云开发 Github Action 进行管理部署。云开发提供了免费的二级域名（未绑定自定义域名时下行速度有限制），同时支持免费绑定开发者自己的自定义域名。

首个环境可享受 1GB 容量和每月 5GB 流量的免费额度，对于访问量不是很大的个人博客应该足够了。如果流量大也没关系，计费是按照具体使用收费的按量付费方式，具体信息可以查看计费价格文档 https://cloud.tencent.com/product/wh/pricing

云开发静态托管部署的网站，还可以使用云开发的提供的一站式 Serverless 后端能力，例如云函数、云数据库、云存储、身份服务等。比如可以在静态托管的个人博客上面使用云函数和云数据库实现评论、留言板功能等，或者可以把博客的内容管理从原来的静态文件部署变为动态内容管理等，拓展的用法非常的多，开发者可以继续深入探索。

## 如何通过 Github Action 一键部署到云开发

下面演示如何将 Github 静态页面自动部署到云开发的静态托管，来获得稳定的访问速度和更多的扩展能力。

例如开发者的个人博客 Github 项目结构如下：

    |-- src
    |-- build
    |-- README.md 

希望将项目下 build 目录生成的静态网站代码部署到云开发这边开通的静态网站托管的根目录下。

## 编写 Github Action 文件
首先在项目目录配置如下的 Github Action 文件 .github/workflows/main.yml，如果已经配置过 Github Action 就不需要重新创建了，然后参考下面的配置填写。

    on: [push] # push 代码时触发

    jobs:
    deploy:
        runs-on: ubuntu-latest
        name: Tencent Cloudbase Github Action Example
        steps:
        - name: Checkout
            uses: actions/checkout@v2
        
        # 使用云开发 Github Action 部署
        - name: Deploy static to Tencent CloudBase
            id: deployStatic
            uses: TencentCloudBase/cloudbase-action@v1
            with:
                # 云开发的访问密钥 secretId 和 secretKey
            secretId: ${{ secrets.SECRET_ID }}
            secretKey: ${{ secrets.SECRET_KEY }}
            # 云开发的环境id
            envId: ${{ secrets.ENV_ID }}
            # Github 项目静态文件的路径
            staticSrcPath: build

可以看到配置中主要用到了  云开发 Github Action 扩展 `TencentCloudBase/cloudbase-action@v1` 来部署静态文件。

注意配置文件中参数部分的 secretId、secretKey 、envId属于敏感信息，需要放在项目的 secret 存储中，这里不用填写真实的值，只需要按照上面实例填写变量即可。

staticSrcPath 这里填写了静态网站构建产生的目录 build，如果想把静态资源部署到云端的某个子目录而不是根目录，可以再配置一个参数 staticDestPath 。

## 配置云开发访问信息

我们还需要在项目的 Secrets 中配置 SECRET_ID、SECRET_KEY、ENV_ID 这几个私密信息，下面是具体的配置方式。

首先要开通云开发静态网站，可以参考开通指南：https://docs.cloudbase.net/hosting/，开通环境后即可得到环境ID ENV_ID，然后在腾讯云 访问管理 页面可以配置一对 API 访问密钥，也就是SECRET_ID、SECRET_KEY。

然后在自己的 Github 项目内的 Setting/Secrets  里设置 SECRET_ID, SECRET_KEY, ENV_ID 信息即可。

![](https://postimg.aliavv.com/picgo/20200427105246.png)


配置完之后就可以提交代码体验自动部署了，每次 git push  Actions 都会自动运行，将项目的静态资源部署到自己的云开发静态托管环境，部署成功之后即可通过云开发提供的二级域名访问来自己的网站。

![](https://postimg.aliavv.com/picgo/20200427105304.png)

## 配置自定义域名
云开发提供的免费的二级域名下行速度有所限制，开发者最好绑定一个自己的域名，绑定域名是免费的，还可以在腾讯云配置一个免费的 SSL 证书，来通过 HTTPS 访问自己的网站。

自定义域名的方法可以参考这篇文档 https://docs.cloudbase.net/hosting/custom-domain.html

![](https://postimg.aliavv.com/picgo/20200427105335.png)


配置完成后，测试下部署在云开发静态托管的网站的访问速度，根据测速数据可以看到各地的访问速度都非常快。

![](https://postimg.aliavv.com/picgo/20200427105349.png)

## 更多扩展玩法

云开发 Tencent CloudBase Github Action 这个扩展会 Github 项目自动部署到云开发环境，目前支持静态托管功能，后续会支持其他资源的部署，比如可以把用 Node JS 、 Java、PHP 等语言开发的服务端项目一键部署到云开发，来获得 Serverless 化的动态网站服务。或者自动化部署带有数据库、前端、后端的全栈应用。

Tencent CloudBase Github Action  扩展市场地址

https://github.com/marketplace/actions/tencent-cloudbase-github-action

Tencent CloudBase Github Action 代码开源地址

https://github.com/TencentCloudBase/cloudbase-action

欢迎大家多多体验、Star 支持或者提交 Issue / Pull request 来参与贡献。