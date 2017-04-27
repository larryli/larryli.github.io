---
ID: 624253
post_title: >
  VC++2008 Express 不需要 Platform SDK
  就能编译 SDL
author: 南 靖男
post_date: 2008-03-01 02:19:22
post_excerpt: ""
layout: post
permalink: 2008/03/624253
published: true
---
给本本重装系统，然后艰难的安装 Visual C++ 2008 中文速成版，非得通过网络安装啊。那个可恶的 ISO 实在是太大。

嗯。重新试了下，2008 Express 虽然会自动安装 .NET 3.5（附带 3.0 外加中文语言包）。但是，安装完毕后可以卸载 3.0 和 3.5 只留 2.0 sp1 就能运行 IDE。至于编译 Win32 程序，似乎也不需要庞大的 Windows Server 2003 Platform SDK。缺少的是 DirectX 5.0 相关的头文件和库（dinput.h;dsound.h;dxguid.lib），这种东西从古老的 Inside DirectX CD 上可以找到，呵呵（也就是 DirectX 5 SDK，在最新的 Platform SDK 和 DirectX SDK 也没有的说）。另外 <a href="http://www.microsoft.com/msdownload/platformsdk/sdkupdate/XPSP2FULLInstall.htm">Windows XP SP2 Platform SDK</a> 也要小的多，百度一下居然找到<a href="http://reactos.bokee.com/494046.html">自己以前的日志</a>。

不知道为什么 <a href="http://www.smorgasbordet.com/pellesc/download.htm">Pelles C 5.0 更新了一个  beta #2  版本</a>。没有找到这个  beta #2 的更新内容，<a href="http://forum.pellesc.de/">官方论坛</a>貌似继续被墙在。