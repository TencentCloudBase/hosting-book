# WordPress 静态化部署到云开发网站托管

> 本文作者：[云开发用户 Handsomedoggy](https://cloud.tencent.com/developer/article/1607761)

相信很多同学都接触过或者使用过博客系统WordPress，WordPress不得不说是一个非常棒的一个CMS，这点是毋庸置疑的，不管是从它的性能上来说还是从它整个的一个功能上。那么本篇文章，就教你如何把一个静态的WP部署到腾讯云的云开发上。

这里就有同学问了，什么是静态？为什么我们要使用静态？

## 1、什么是静态？-----我们这里所说的静态，是指静态的web网站。

它的每一个页面都是由html文件配合CSS、Javascript或其他媒体元素组成，这类型的网站，每一次修改都是需要重新的部署，名字上我们也了解到，静态嘛，固定不动。不过同学也不要理解成静态网站就是从视觉上的静态了。

## 2、为什么我们要使用静态WordPess？------关于这个问题，其实静态跟动态可以说是各有所长。
- 稳定性---因为是静态的，所以它的页面内容是比较稳定的，他不会因为程序上的某些错误就会导致一些显示的不正常。

- 安全性---静态是特别安全的，因为它们本身就只是html文件，不会涉及到任何的数据库等。

- 速度---静态文件的加载速度比动态文件快，就好比如，我们使用一个php程序，它需要调用数据库，需要去执行我们给他编写好的指令，静态文件没有这些步骤。再然后就是可以配合CDN(内容分发系统)，做到更快的网站访问速度。

- 费用---静态文件使用的资源较少。

这里有的同学又有问题了，静态那么好，为什么我们还要使用动态的呢？
就如我上面所说，静态跟动态各有所长，下面我们来说说WordPress静态化后的缺点:

1. 评论系统、会员模块、各种各样的插件等一系列需要使用到PHP和数据库的所有模块都会失效，如果你经常需要互动之类的，那么这个静态WP可能不是很适合你，或许你也可以找到其他的解决方案。

2. 内容改变需要重新部署，因为是静态的文件，所以你做的每次改动都需要重新部署到我们的云开发上，相对来说比较麻烦，如果你是经常更新甚至是日更，那么这个静态WP可能不是很适合你。

综上所述，此方案比较适合不经常更新且具有展示性需求使用的同学使用。介绍了那么多，我们开始进入正题！
## 安装依赖环境
首先我们需要安装Node.js 和 npm，可参考node.js安装指南 

再然后我们需要安装云开发的CLI

    npm install -g @cloudbase/cli //此前需要安装 Node.js

安装完成后，我们需要在我们的本地部署一个PHP环境以及安装好我们的WP。本地环境可以使用PHPSTUDY或者WAMPSERVER 

我们安装好本地环境后，启动我们的本地web服务

![](https://postimg.aliavv.com/picgo/20200427122717.png)

点击网站---管理---根目录  就可以进入到我们的本地网站根目录啦
之后我们到WordPress官网 下载Wordpress程序，打开并把wordpress文件夹解压到本地网站的根目录。

![](https://postimg.aliavv.com/picgo/20200427122729.png)

紧接着我们到浏览器，访问我们的wordpress

![](https://postimg.aliavv.com/picgo/20200427122740.png)

点击现在开始我们会看到要求我们填写数据库信息。我们先到我们的本地环境上创建一个数据库

![](https://postimg.aliavv.com/picgo/20200427122749.png)


紧接着我们输入我们的数据库信息,数据库主机我们使用默认的localhost， 表前缀无需改动
点击提交后我们就会到站点信息补充，填写好我们的管理员用户&密码&站点名称等 我们点击安装

![](https://postimg.aliavv.com/picgo/20200427122756.png)

安装完成后，有的同学点击登录可能会 出现该网页无法正常运作 localhost 目前无法处理此请求。HTTP ERROR 500的错误，

这里我们可以在地址栏输入http://本地链接/wordpress/ 先进入我们的主页面看看,不出意外的话同学们都已经显示出我们的主页了。


之后我们再访问 http://本地/wordpress/wp-admin/   (http://localhost/wordpress/wp-admin/)就可以进入我们的后台管理页面啦，输入我们之前所填写的用户名与密码即可登录到后台管理页面。(本地请替换为localhost)

有的同学的WP页面会出现一些PHP相关的错误或者Warnning，可以到本地环境的php.ini更改一下错误显示。
使用phpstudy的同学可以到 **设置--配置文件--php.ini**，点击php7.3.4ns可以进入到php.ini。

WAMP的同学可以单击任务栏WAMP小图标，找到php.ini 。我们进入到php.ini后，搜索 error_reporting 并把 `error_reporting=E_ALL` 改成

`error_reporting=E_ALL & ~E_DEPRECATED & ~E_STRICT`

继续搜索 `display_errors` 并把`display_errors=On`改成`display_errors=Off`

继续搜索 log_errors 并把`log_errors=On`改成`log_errors=Off`

之后我们重启一下web服务，再访问我们的主页就不会出现错误提示啦！

紧接着我们安装三个插件

- [wp2static-7.0-alpha-004 (3).zip](https://ask.qcloudimg.com/draft/6685282/nszql0s44g.zip)
- [wp2static-addon-zip-1.0-alpha-2 (1).zip](https://ask.qcloudimg.com/draft/6685282/xekdxh169g.zip)
- [wenprise-pinyin-slug.1.4.13.zip](https://ask.qcloudimg.com/draft/6685282/cz3c5266eu.zip)

下载上面的附件后，到后台管理的插件--添加插件--上传插件，依次导入安装并启用插件。

第一个插件是WP2Static 这个插件可以帮助我们把WP转换为静态文件

第二个插件是Wenprise Pinyin Slug 这个插件可以把中文的名称转换为拼音(在路径上的转换会用到)

之后我们就可以开始我们的创作啦！

![](https://postimg.aliavv.com/picgo/20200427122952.png)

我随便创建了两篇文章用于测试使用，并添加了附件与图片
之后我们到插件wp2static插件进行静态化操作。在使用插件之前，我们到我们腾讯云的控制台找到云开发 并创建好云环境，再进入云环境把网站托管打开。如无意外的话我们可以看到我们的云环境ID 我的是ykc-151533

然后我们进入到插件页面

![](https://postimg.aliavv.com/picgo/20200427123009.png)

紧接着我们点击Option下面的Jobs，把interval选择为every minute（这里的意思是插件开始运作的时间），再点击Manually Enqueue Jobs Now（手动添加进执行队列）

![](https://postimg.aliavv.com/picgo/20200427123014.png)

紧接着我们等待片刻，时不时点击一下Refresh page,等我们看到所有工作的Status(状态)都显示completed(完成)的时候，我们进入下面的ZIP(在logs下面)，选择download zip。下载完后，这个zip文件就是我们WP的静态文件啦

紧接着我们开始把这个静态文件部署到我们的云开发，我们解压文件到一个目录,我解压到了E:\test 如果不出意外的话你会看到一个index.html wordpress wp-content index.php等文件夹

然后我们打开终端 进入他的上级目录

    cd D:\

紧接着我们登录我们的Cloudbase CLI 我们输入命令

    tcb login

会自动跳转到腾讯云页面进行授权，授权结束后，我们输入

    tcb hosting:deploy test -e 你云环境ID

我的是ykc-151533 所以我输入

    tcb hosting:deploy test -e ykc-151533

之后就会把我们整个test目录上传到云环境啦，然后我们再输入终端命令

    tcb hosting:detail -e ykc-151533(替换成自己的ID噢！) //查看静态网站域名

我的是https://ykc-151533.tcloudbaseapp.com 


![](https://postimg.aliavv.com/picgo/20200427123038.png)

可以看得到不论是英文还是中文都是正常显示的一个状态，附件也是可用的
本次部署就完成啦！因为云开发默认域名仅供测试使用，限制下行速度10KB/S。如您需要对外正式提供网站服务，请绑定您已备案的自定义域名。所以打开速度可能会有一点点慢的，有条件的同学可以绑定自己的域名啦！

好了，本次的分享就到这里了，有想法或者对本次的部署有什么疑问的同学可以到下面的评论区评论啦！