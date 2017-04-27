---
ID: 637113
post_title: 装好了 IspCP，累了好几天
author: 南 靖男
post_date: 2009-02-23 23:16:11
post_excerpt: ""
layout: post
permalink: 2009/02/637113
published: true
---
<p>当然这几天没写日志主要原因倒是 Flock 的 blog 编辑器不能设置账户了。正好我重装了系统。没办法，用 Live Writer 吧。</p>  <p>言归正传，一开始的选择就是 <a href="http://www.isp-control.net/">ispcp</a>，结果安装脚本卡死了（原因后面再说）。只好再去找已经停滞的 <a href="http://vhcs.net/">VHCS</a>，虽然有现成的中文带注解和截图的 <a href="http://wiki.ubuntu.org.cn/index.php?title=UbuntuHelp:VHCS/zh&amp;variant=zh-cn">ubuntu 专用帮助</a>，还是问题多多，折腾了一两天才弄好。然后又回过头来弄 ispcp。结果很偶然的发现问题所在了。</p>  <p>1、一定要在实际控制台上运行安装脚本，而不是虚拟终端。没办法，我已经很习惯使用 putty 了。</p>  <p>2、要选择 fastcgi 模式，而不是默认的 fcgid。</p>  <p>另外，还有一些大的小的诸如中文乱码之类的毛病。服务器存在的 Tomcat/mod_jk 虚拟主机和 Zend Optimizer 乃至 mcrypt 扩展都是样样烦人，要一一调整。</p>  <p>思前想后，发觉我不是需要重新弄一个 blog（我实在找不到其他比较好又稳定的 wordpress 托管），而是把自己关于技术上一些琐碎的 tips 分门别类的记录下来。所以，干脆就 <a href="http://sites.google.com/site/larryli">Google sites</a> 好了。这里还是继续这样杂乱无章的状态，反正也没什么人看，呵呵。真正需要的时候，能有一个团队围绕一个或者多个主题展开倒是值得考虑。一个人嘛，就这样吧。</p>