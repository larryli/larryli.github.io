---
ID: 644942
post_title: '使用 Let&#8217;s Encrypt 证书'
author: 南 靖男
post_date: 2015-12-22 17:25:22
post_excerpt: ""
layout: post
permalink: 2015/12/644942
published: true
---
主站切换到 <a href="https://letsencrypt.org">Let's Encrypt</a> 自动颁发的免费证书。

目前公测期间，证书只有 90 天有效期，但可以使用 crontab 脚本自动在服务器上定时 renew。

不过，颁发证书本身有 IP 和域名的限制。

&nbsp;