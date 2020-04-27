# 如何借助 Gitlab CI 将项目部署到云开发静态网站托管

**云开发静态托管是云开发提供的静态网站托管的能力，静态资源（HTML、CSS、JavaScript、字体等）的分发由腾讯云对象存储 COS 和拥有多个边缘网点的腾讯云 CDN 提供支持**

本文使用了`create-react-app`创建了一个React应用，并把该应用部署到腾讯云的静态网站托管。

## **作者介绍**

钟炜达，任职于腾讯在线教育部IMWEB团队，是一名前端开发工程师。有丰富Web应用开发经验和在前端工程化方面有较多的实践。

## **GitLab中创建 test-cra 项目**

到GitLab首页，点击`NewProject`创建新的工程

​
![](https://postimg.aliavv.com/picgo/20200427103933.png)

`Project Name`和`Project Slug`都填上`test-cra`，点击`Create Project`

​![](https://postimg.aliavv.com/picgo/20200427103933.png)


## **创建web应用**

在本地环境通过`create-react-app`创建了一个名为`test-cra`的项目

```js
yarn create react-app test-cra
```

设置git相关设置，并上传应用到GitLab

```js
cd test-cra
git init
# 这里需要注意username为你的gitlab账户名
git remote add origin git@gitlab.com:username/test-cra.git
git add .
git commit -m "Initial commit"
git push -u origin master
```

接下来到腾讯云中创建云开发环境

## **创建云开发环境**

输入网址：[https://console.cloud.tencent.com/tcb/env/index](https://console.cloud.tencent.com/tcb/env/index)，如果没有授权会弹出以下画面。

![](https://postimg.aliavv.com/picgo/20200427103933.png)

点击`访问管理`，进入授权。

创建一个云开发环境。这里命名环境为`test-cra`。

​
![](https://postimg.aliavv.com/picgo/20200427104148.png)


## **设置SecretId和SecretKey**

输入网址：[https://console.cloud.tencent.com/cam/capi](https://console.cloud.tencent.com/cam/capi)点击新建秘钥即可。

![](https://postimg.aliavv.com/picgo/20200427104240.jpg)


## **GitLab CI设置**

SecretId和SecretKey属于敏感数据，不应该直接写到CI配置文件中。

回到刚刚创建的GitLab项目，找到Settings->CI/CD

![](https://postimg.aliavv.com/picgo/20200427104258.jpg)


找到Variables项如图新建3个key，SecretId、SecretKey和EnvId。并输入对应的value值。注意必须要开启`protected`和`masked`，这样能有效保证数据保密和安全。

​
![](https://postimg.aliavv.com/picgo/20200427104315.jpg)


在云开发面板中，找到环境设置中的环境ID。EnvId的value为环境ID

​
![](https://postimg.aliavv.com/picgo/20200427104636.png)

## **创建.gitlab-ci.yml配置文件**

在本地工程_test-cra_的根目录中创建`.gitlab-ci.yml`文件

![](https://postimg.aliavv.com/picgo/20200427104647.png)


`.gitlab-ci.yml`配置文件如下，这里可查看更多的[gitlab ci 配置](https://gitlab.com/help/ci/yaml/README)

```js
image: node:12.16.2
stages:
  - build
  - deploy

build:
  stage: build
  script:
    - npm i
    - npm run build
  artifacts:
    paths:
      - ./build/
  only:
    - maste

deploy:
  stage: deploy
  script:
    - cd ./build
    - npm i -g @cloudbase/cli
    - tcb login --apiKeyId $SecretId --apiKey $SecretKey
    - tcb hosting:deploy -e $EnvId
  only:
    - master
```

- 使用node12的镜像作为基础环境
- 整个CI流程有2个`stage`
1. 构建阶段（build）：生成构建产物，并把构建产物进行存档（artifacts操作）
2. 部署阶段（deploy）：
    1. 需要使用腾讯云提供的cli工具（@cloudbase/cli）
    2. 使用API秘钥直接登录，这里需要使用到上一步的`SecretId`和`SecretKey`环境变量
    3. 进入构建产物目录（这里为`./build`目录），执行全量部署。这里需要使用上一步的`EnvId`环境变量。

更多的`tcb`部署静态网站方法可以在：[http://docs.cloudbase.net/cli/hosting.html](http://docs.cloudbase.net/cli/hosting.html)进行查看。

## **push到远程仓库触发构建**

​
![](https://postimg.aliavv.com/picgo/20200427104701.png)


查看CI结果，显示upload成功。

​
![](https://postimg.aliavv.com/picgo/20200427104717.png)


打开[https://console.cloud.tencent.com/tcb/hosting](https://console.cloud.tencent.com/tcb/hosting)，选择设置，点击默认域名即可访问刚刚部署的web应用。

​

![](https://postimg.aliavv.com/picgo/20200427104727.png)
​
![](https://postimg.aliavv.com/picgo/20200427104733.png)