---
ID: 645619
post_title: '完全使用 Let&#8217;s Encrypt 证书'
author: 南 靖男
post_date: 2017-04-10 18:41:21
post_excerpt: ""
layout: post
permalink: 2017/04/645619
published: true
---
因为众所周知的原因，StartSSL 已经不合适再继续使用了。而且 <a href="https://letsencrypt.org/">Let's Encrypt</a> 也足够好用。

Ubuntu 下直接使用 ppa:certbot/certbot 即可。只是因为脚本各种更新导致配置凌乱，现在应该稳定了。

并且，出于安全原因，90 天有效的证书似乎更好~