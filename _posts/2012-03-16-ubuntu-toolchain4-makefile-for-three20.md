---
ID: 644634
post_title: Three20 Makefile for Ubuntu toolchain4
author: 南 靖男
post_date: 2012-03-16 02:38:11
post_excerpt: ""
layout: post
permalink: https://larryli.cn/2012/03/644634
published: true
---
<a href="https://github.com/facebook/three20" title="Three20">Three20</a> 是 iOS 上一个基于 uri 设计的开发框架。<a href="https://github.com/javacom/toolchain4" title="toolchain4">toolchain4</a> 是 Ubuntu 下 iOS 的交叉编译环境。
由于 Three20 没有提供 Makefile 文件，只有 Apple Xcode 项目配置文件，就无法直接在 toolchain4 中编译。
花了一晚上时间写 <a href="/download/Three20.toolchain4.Makefile.tar.bz2" title="Three20.toolchain4.Makefile.tar.bz2">Makefile</a>，问题还存在很多，但至少是可以编译 Three20 自带的两个 sample 成功。另外，自己做的一个小应用，也能编译成功。运行就或多或少有 Bug。
另外需要注意的是 Info.plist 文件需要手工处理一下 $ 变量，toolchain4 是不会自动处理的。