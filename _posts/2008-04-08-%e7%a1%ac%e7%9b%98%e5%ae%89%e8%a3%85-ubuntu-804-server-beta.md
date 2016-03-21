---
ID: 626074
post_title: 硬盘安装 Ubuntu 8.04 server beta
author: 南 靖男
post_date: 2008-04-08 23:18:29
post_excerpt: ""
layout: post
permalink: https://larryli.cn/2008/04/626074
published: true
---
没必要为了这个 Beta 版本刻一张盘，我的 Ubuntu CD 已经足够多了。但手头有空余的硬盘，所以就想试试硬盘安装，折腾了一晚上，总算 OK 了。

首先是给硬盘分区，我是随便找的一张以前的 livecd 从光驱启动，只挂载那块空硬盘。分区需要注意的是，<strong>存放 iso 镜像文件的分区在安装时是不能挂载的</strong>。所以，至少需要两个分区才能硬盘安装。

建议将 hda1 分配 1~2G 空间用来存放 iso，hda2 作为安装时的根目录。分区完毕后格式化为 ext3。
<code># fdisk /dev/hda
&gt; n
p
1
1
+1023M
&gt; n
p
2
124
xxxx
&gt; w
&gt; q
# mkfs.ext3 /dev/hda1
# mkfs.ext3 /dev/hda2</code>

完成之后，挂载 hda1 安装 grub。
<code># mkdir /hd1
# mount /dev/hda1 /hd1
# mkdir /hd1/boot
# mkdir /hd1/boot/grub
# cp /lib/grub/pc-i386/* /hd1/boot/grub
# grub
&gt; root (hd0,0)
&gt; setup (hd0)
&gt; quit</code>

可以手工建立一个 menu.lst 启动菜单。
<code># nano /hd1/boot/grub/menu.lst</code>

内容如下：
<code>title install
root (hd0,0)
kernel /vmlinuz boot=casper find_iso/filename=/ubuntu-8.04-beta-server-i386.iso
initrd /initrd.gz
boot</code>

现在可以从网络下载启动映像和 iso 到 /hd1 目录下，也可以将硬盘挂到其他系统下复制文件。这里必须使用专门的 vmlinuz 和 initrd.gz 而不是 iso 中的版本（Desktop 版本直接使用 iso 中的可以）。下载地址在每个 ubuntu 镜像站点的 main/installer-i386/current/images/hd-media/ 目录下可以找到，比如<a href="http://mirror.lupaworld.com/ubuntu/dists/hardy/main/installer-i386/current/images/hd-media/">这个</a>。

完成后重启系统就可以直接进入安装。正如一开始提到的，在安装时不能挂在 hda1，因为安装程序已经将它挂载到 /hd-media 下。