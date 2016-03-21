---
ID: 262671
post_title: Subversion of ReactOS
author: 南 靖男
post_date: 2005-04-15 22:00:24
post_excerpt: ""
layout: post
permalink: https://larryli.cn/2005/04/262671
published: true
---
svn 是最新版本的协作开发软件，cvs 的下一代。
ReactOS 从 2004 年底开始使用 svn 服务器地址为：svn://svn.reactos.com
在 SVN 主页 <a href="http://subversion.tigris.org/">http://subversion.tigris.org/</a> 下载 Windows 版本，压缩包或者安装版都可以。
完了，最好将 svn 的 bin 目录加入 PATH 环境变量：SET PATH=%PATH%;C:svnbin
然后，在命令行，CD 到准备下载源代码的目录
svn checkout svn://svn.reactos.com/trunk/reactos ros-svn
这样就可以将当前开发版本的 ReactOS 源代码下载到 ros-svn 目录。
由于网络速度的限制，而目前源代码有两三百兆大小，直接 svn checkout 很可能需要三到五个小时。
所以在 www.sf.net 下载 ReactOS 的最新发布的源代码包，然后进入目录直接 svn update 会快很多。