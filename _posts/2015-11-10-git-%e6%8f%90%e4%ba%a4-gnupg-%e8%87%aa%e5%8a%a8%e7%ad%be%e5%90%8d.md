---
ID: 644926
post_title: Git 提交 GnuPG 自动签名
author: 南 靖男
post_date: 2015-11-10 22:37:26
post_excerpt: ""
layout: post
permalink: 2015/11/644926
published: true
---
一般来说使用 <code>git commit -S</code> 就调用 gpg 工具自动搜索 <code>user.name&lt;user.email&gt;</code> 对应的私钥来签名提交。

git 2.0 以上版本提供了 <code>commit.gpgsign</code> 设置可以自动打开 gpg 签名选项。

然后配合 <code>user.signingkey</code> 就可以设置默认的 key 来自动签名了。

<pre>git config --global user.name "Larry Li"
git config --global user.email larryli@qq.com
git config --global user.signingkey 2D8B022C
git config --global commit.gpgsign true</pre>

密钥 <code>2D8B022C</code> 可以通过 <code>gpg -K</code> 查看可用的私钥。