# 云开发网站托管如何绑定域名


如果我们访问站点是通过云开发提供的默认域名，首先默认域名访问的时候是会有限行访问速度的限制，其次，默认域名并不是非常好记，所以，这篇文章我们将介绍下，如何在云开发静态托管绑定静态域名。

### 一、申请域名

首先，我们需要申请一个可供访问的站点域名。可以选择在[腾讯云域名注册](https://buy.cloud.tencent.com/domain)上注册一个自己喜欢并且可供使用的域名。

### 二、申请SSL证书

>  什么是SSL证书？
>  安全套接字层 (SSL) 证书（有时称为数字证书）用于在浏览器或用户计算机与服务器或网站之间建立加密连接。SSL连接可保护在每次访问（称为会话）期间交换的敏感数据（例如信用卡信息），以防被非授权方拦截。

简单来说，就是部署了SSL证书的站点，可以让用户的访问的时候更加安全。一般来说，SSL证书是收费的，腾讯云提供可供免费使用的SSL证书。

在[腾讯云的SSL证书控制台](https://console.cloud.tencent.com/ssl)中，点击申请免费的SSL证书：

![配图](https://ask.qcloudimg.com/http-save/4744530/w19hcj85la.png)

然后，在通用名称中填写刚刚申请好的域名，并按照提示填写剩余的填写项：

![配图2](https://ask.qcloudimg.com/http-save/4744530/da1q3m2qou.png)

进入审核阶段，等待会，就会看到审核成功之后的界面：

![](https://postimg.aliavv.com/picgo/20200426173618.png)

### 三、绑定域名和SSL证书

回到[云开发静态网站托管](https://console.cloud.tencent.com/tcb/hosting)界面，在_设置_一栏中，点击添加：

![](https://postimg.aliavv.com/picgo/20200426173641.png)

填写刚刚申请好的域名，选择我们在这个域名上绑定的SSL证书，点击确定添加即可。

![](https://postimg.aliavv.com/picgo/20200426173654.png)

等待域名和证书部署完成后，就可以看到域名对应的CNAME值。

![](https://postimg.aliavv.com/picgo/20200426173704.png)

### 四、添加系统域名解析

想要在浏览器输入域名能直接访问到我们的网站，我们需要给访问的域名绑定DNS解析，让浏览器知道，这个域名其实是对应我部署好的站点。

进入[腾讯云的DNS域名解析](https://console.cloud.tencent.com/cns)控制台，选择我们注册好的域名，点击解析：

![](https://postimg.aliavv.com/picgo/20200426173716.png)

在域名解析界面，添加在第三部我们拿到的绑定域名的CNAME值：

![](https://postimg.aliavv.com/picgo/20200426173724.png)

填好好后，访问域名就可以直接看到我们部署的静态网站了。