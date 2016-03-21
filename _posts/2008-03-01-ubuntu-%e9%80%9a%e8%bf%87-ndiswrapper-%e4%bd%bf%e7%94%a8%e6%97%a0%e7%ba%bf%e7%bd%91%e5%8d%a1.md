---
ID: 624270
post_title: >
  Ubuntu 通过 Ndiswrapper
  使用无线网卡
author: 南 靖男
post_date: 2008-03-01 18:21:11
post_excerpt: ""
layout: post
permalink: https://larryli.cn/2008/03/624270
published: true
---
首先找到 Windows 下的 .inf 文件，我的是 neti2220.inf 貌似在 NTFS 盘上不能直接用，需要先复制到 home 目录。然后 sudo apt-get install ndisgtk，再到“系统”－》“系统管理”－》“Windows Wireless Drivers”里面 Install New Driver，成功后会显示驱动名称和硬件是否存在。虽然 Ubuntu 7.10 的帮助就此结束，但事情还没完，需要继续操作。

sudo ndiswrapper -l 的操作只是确认 ndisgtk 的结果。然后 sudo ndiswrapper -m 后 sudo modprobe ndiswrapper系统应该可以找到无线网卡了，在 GNOME 的网卡管理会出现无线网络已经找到的 AP，点击就可以连接。需要密钥自然有对话框来填入。

最后的操作是将  ndiswrapper  加入  modules：sudo gedit /etc/modules