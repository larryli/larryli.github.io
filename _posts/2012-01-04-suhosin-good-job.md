---
ID: 644577
post_title: Suhosin, Good job!
author: 南 靖男
post_date: 2012-01-04 13:53:55
post_excerpt: ""
layout: post
permalink: https://larryli.cn/2012/01/644577
published: true
---
2011 年末传出动态语言大范围的 <a href="http://www.laruence.com/2011/12/29/2412.html">Hash DOS</a> 攻击漏洞。年后上班一看到就发现宣传都是说该漏洞是核弹级别的。正在考虑是否真的需要放弃 apt 源，手工 patch 源码更新时，从漏洞的传播源看到有人<a href="http://nikic.github.com/2011/12/28/Supercolliding-a-PHP-array.html#dsq-comment-body-396715488">评论</a>提到了 Suhosin。
是的，Suhosin 不亏为保护神，确实早已经设置了 <a href="http://www.hardened-php.net/suhosin/configuration.html#suhosin.post.max_vars">suhosin.post.max_vars</a> 限制。
嗯，不用麻烦了。难怪出现这种所谓核弹级别的漏洞，apt 源半点反应都没。