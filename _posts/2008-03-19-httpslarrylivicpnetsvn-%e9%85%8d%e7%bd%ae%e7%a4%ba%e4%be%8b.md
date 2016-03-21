---
ID: 625176
post_title: >
  https://larryli.vicp.net/svn
  配置示例
author: 南 靖男
post_date: 2008-03-19 22:19:44
post_excerpt: ""
layout: post
permalink: https://larryli.cn/2008/03/625176
published: true
---
<code># http 配置
&lt;VirtualHost *:80&gt;
ServerAdmin larryli@qq.com
# 使用独立的虚拟主机目录
DocumentRoot /xampplite/larryli/htdocs
ServerName larryli.vicp.net
# logs 也放在独立目录中
ErrorLog /xampplite/larryli/logs/error.log
CustomLog /xampplite/larryli/logs/access.log common
&lt;Directory "/xampplite/larryli/htdocs"&gt;
# 一般的安全设置
Options FollowSymLinks Includes
AllowOverride All
Order allow,deny
Allow from all
&lt;/Directory&gt;
&lt;IfModule dav_svn_module&gt;
&lt;Location /svn&gt;
DAV svn
# svn 也放在独立目录下
SVNPath /xampplite/larryli/svn
AuthType Basic
AuthName "larryli subversion repository"
# svn-none 是一个空文件，这样就只允许 http://larryli.vicp.net/svn 读操作，禁止写
AuthUserFile /xampplite/larryli/conf/svn-none
&lt;LimitExcept GET PROPFIND OPTIONS REPORT&gt;
Require valid-user
&lt;/LimitExcept&gt;
&lt;/Location&gt;
&lt;/IfModule&gt;
&lt;/VirtualHost&gt;
# https 配置
&lt;VirtualHost *:443&gt;
SSLEngine on
ServerSignature On
# 分开设置密钥
SSLCertificateFile /xampplite/larryli/conf/server.crt
SSLCertificateKeyFile /xampplite/larryli/conf/server.key
ServerAdmin larryli@qq.com
DocumentRoot /xampplite/larryli/htdocs
ServerName larryli.vicp.net
# SSL 日志
ErrorLog /xampplite/larryli/logs/ssl-error.log
CustomLog /xampplite/larryli/logs/ssl-access.log common
&lt;Directory "/xampplite/larryli/htdocs"&gt;
Options FollowSymLinks Includes
AllowOverride All
Order allow,deny
Allow from all
&lt;/Directory&gt;
&lt;IfModule dav_svn_module&gt;
&lt;Location /svn&gt;
DAV svn
SVNPath /xampplite/larryli/svn
AuthType Basic
AuthName "larryli subversion repository"
# 用户认证文件
AuthUserFile /xampplite/larryli/conf/svn-passwd
# https 下读写都需要认证
Require valid-user
&lt;/Location&gt;
&lt;/IfModule&gt;
&lt;/VirtualHost&gt;</code>