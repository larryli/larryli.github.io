---
ID: 629720
post_title: Ubuntu 下使用 VPN
author: 南 靖男
post_date: 2008-07-21 21:30:32
post_excerpt: ""
layout: post
permalink: https://larryli.cn/2008/07/629720
published: true
---
参考<a href="http://chinagfw.blogspot.com/2008/07/ubuntu-vpn.html">这篇文章</a>安装下面的软件包：
sudo apt-get install pptp-linux
sudo apt-get install network-manager-pptp
sudo apt-get install network-manager-vpnc
sudo apt-get install network-manager-openvpn
实际上只需要 network-manager-pptp 就可以使用 windows vpn 了（会自动安装第一个包）。后面两个包针对是&nbsp; Cisco 的 vpn 和 OpenVPN。
安装完后，点击网卡图标就会出现 VPN 连接菜单。然后进配置界面，选择 PPTP tunnel 就是。剩下的熟悉 Windows VPN 配置就很容易了。
配置完，就会看见连接，点击，填帐号和密码。
稍等片刻，网卡图标右下出现一把小锁。

   <div class="flockcredit" style="text-align: right; color: #CCC; font-size: x-small;">用 <a href="http://www.flock.com/blogged-with-flock" style="color: #999; font-weight: bold;" target="_new" title="Flock Browser">Flock 浏览器</a> 创建</div>