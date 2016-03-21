---
ID: 626405
post_title: 开通了 Google App Engine
author: 南 靖男
post_date: 2008-04-19 21:32:53
post_excerpt: ""
layout: post
permalink: https://larryli.cn/2008/04/626405
published: true
---
随便注册了一个 <a href="http://xsk.appspot.com/">XSK</a> <img src="http://allgames.gamesh.com/srwbbs/images/face/XSK.gif" height="32" width="32" /> 下面是一些截图：

这是应用列表。

<a href="https://larryli.cn/wp-content/uploads/50/5051/2008/04/appengine1.png" title="应用列表"><img src="https://larryli.cn/wp-content/uploads/50/5051/2008/04/appengine1.thumbnail.png" alt="应用列表" /></a>

每一个应用有控制面板。

<a href="https://larryli.cn/wp-content/uploads/50/5051/2008/04/appengine2.png" title="控制面板"><img src="https://larryli.cn/wp-content/uploads/50/5051/2008/04/appengine2.thumbnail.png" alt="控制面板" /></a>

Logs 里面有错误日志，Index 和 Data Viewer 必须使用 Google 的数据库才有内容。

应用设置可以设置应用的名称，以及能够使 Google 帐户的范围，默认是所有，必须开通 Google Apps 的域名可以选择限制。

开发者就是能上传和访问这个东东的电子邮件了。

有意思的是版本控制，App Engine 应用版本号有两个，一个是主，由用户在 app.yaml 中指定，另一个是副版本号，每一次 update 就会自动加 1。这里就可以控制主版本号的切换，另外每一个版本实现都有独立的 domain 访问。

<a href="https://larryli.cn/wp-content/uploads/50/5051/2008/04/appengine3.png" title="版本控制"><img src="https://larryli.cn/wp-content/uploads/50/5051/2008/04/appengine3.thumbnail.png" alt="版本控制" /></a>

嗯。发表这篇日志的时候，访问 http://1.3.xsk.appspot.com/ 和 http://xsk.appspot.com/ 是一样的。

<a href="https://larryli.cn/wp-content/uploads/50/5051/2008/04/appengine4.png" title="XSK XSK"><img src="https://larryli.cn/wp-content/uploads/50/5051/2008/04/appengine4.thumbnail.png" alt="XSK XSK" /></a>

需要注意的是，在 py 文件必须指定编码才能使用中文（虽然本地测试不会有问题，但是提交到 appengine 会报错），详细内容在<a href="http://www.python.org/dev/peps/pep-0263/" title="Defining Python Source Code Encodings">这篇文档</a>里。

<code>#!/usr/bin/python
# vim: set fileencoding=utf-8 :</code>

实际上我的代码里面很早就存在这样的东东了，呵呵。