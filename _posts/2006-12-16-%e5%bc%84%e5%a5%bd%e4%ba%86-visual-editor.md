---
ID: 263013
post_title: 弄好了 Visual Editor
author: 南 靖男
post_date: 2006-12-16 22:39:03
post_excerpt: ""
layout: post
permalink: https://larryli.cn/2006/12/263013
published: true
---
<p align="left">在 xubuntu 下 apt-get 安装好 eclipse，然后下载 emf-sdo-runtime-2.2.0.zip GEF-runtime-3.2.zip JEM-runtime-1.2.2_jem.zip 和 VE-runtime-1.2.2_jem.zip 直接解压到 /usr/lib/ 也就是安装到 /usr/lib/eclipse 下。</p>
 结果一启动 Visual Java 编辑就出现 An internal error occurred during: "Create Remote VM for Visual Editor for Java".
也就是中文“无法为 Visual Editor 创建 Java 远程 VM”。
因为事先也解压了 NLpack1 得到是半中半英的错误提示，根本就没法在 google 找到任何有效信息。
只好删除所有东东，重新下载解压，折腾了大半天然后搜寻错误所在。
结果在 <a href="https://bugs.eclipse.org/bugs/show_bug.cgi?id=117898">https://bugs.eclipse.org/bugs/show_bug.cgi?id=117898</a> 终于看到了有人提到 /etc/hosts
看了一下 xubuntu 默认的 hosts 果然没有设置 127.0.0.1 localhost 只是指到我的机器名。
增加 127.0.0.1 后面增加一个 localhost，再启动，OK 了。真是的，奇奇怪怪的毛病。