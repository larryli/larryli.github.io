---
ID: 644775
post_title: >
  Raspberry Pi Coder 使用 StartSSL
  证书
author: 南 靖男
post_date: 2013-09-16 14:15:42
post_excerpt: ""
layout: post
permalink: https://larryli.cn/2013/09/644775
published: true
---
Google Creative Lab 为 Raspberry Pi 提供了 <a href="http://goo.gl/coder">Coder</a> 工具，默认是使用 https 访问，用的是自动生成的自签名证书。

我们知道 <a href="http://www.startssl.com">StartSSL</a> 是免费为个人提供 SSL 证书的，所以可以将 Coder 的自签名证书替换为 StartSSL 的签名证书。

Coder 的证书是放在 /home/coder/coder-dist/coder-base/certs 名称分为为 server.cert 证书和 server.key 私钥。需要注意的是 Coder 目前只支持 PKCS #8 格式的私钥，需要转换。

<code>openssl pkcs8 -topk8 -inform PEM -in startssl.key -outform PEM -nocrypt -out server.key</code>

另外，cert 证书不支持根证书拼接，直接使用 StartSSL 提供的即可。

最后，需要注意两个文件的属主是 coder，key 私钥文件的权限是 600。