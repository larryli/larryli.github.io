---
ID: 644749
post_title: >
  自己架设了一个在线 RSS
  阅读器
author: 南 靖男
post_date: 2013-03-27 23:07:35
post_excerpt: ""
layout: post
permalink: 2013/03/644749
published: true
---
作为 Google Reader 的重度用户，真的无法接受 Google 关停 Reader 的决定。

对于我来说，90% 的新闻资讯都是来自于 RSS。这其中还有相当分量的技术内容。

GReader 的好处其一是来自 RSS 统一阅读，快速又直接的阅读最新的文章。而且这基本上是我感兴趣的。

其二是历史功能。是的，Google 存储了所有 RSS。使得已经消失的 Atom 继续存在于 Reader 中。只要你曾经订阅过，它就存在。

而现在，它即将消失。

同样在 Reader 上看到<a href="http://seo.g2soft.net/2013/03/25/google-reader.html">别人的文章</a>推荐了 <a href="http://selfoss.aditu.de/">selfoss</a>。自己架设了<a href="https://reader.larryli.cn/">一个</a>（习惯性使用 https，国外产品对此支持一直很不错）。

问题不少。

首先，OPML 导入功能有问题。我原本给一个 ATOM 设置了好几个 tag，这些 tag 没有自动合并。而是存在好几个不同的 ATOM。

其次是抓取功能。没有提供命令行接口，而是采用前台链接访问的方式。因为我的订阅列表很多，而且有大量的失效内容，处理时间会很长，基本上会超过 Web 服务器的最大处理时间。

最后是阅读功能。快捷键有一点不同，需要适应。而文章的分栏阅读界面也需要适应。