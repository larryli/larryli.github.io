---
ID: 625142
post_title: >
  Ubuntu 下安装 Subversion https
  服务器
author: 南 靖男
post_date: 2008-03-18 19:59:20
post_excerpt: ""
layout: post
permalink: 2008/03/625142
published: true
---
首先是安装 Apache2，Ubuntu 上默认安装的 Apache2 就已经带上 ssl 模块。
<code>sudo apt-get install apache2</code>
使用 a2emod 开启模块。
<code>sudo a2enmod ssl</code>
https 必须提供一个站点密钥，一般情况下使用如下命令即可。
<code>apache2-ssl-certificate</code>
但是当前的 ubuntu 版本存在 Bug 遗失了该工具，只能使用 openssl 手工生成。
<code>sudo openssl req -x509 -newkey rsa:1024 -keyout apache.pem -out apache.pem -nodes -days 999</code>
记得在 Common Name 中填写你的域名。
<code>Common Name (eg, YOUR name): larryli.vicp.net</code>
完成后将当前目录下的 apache.pem 文件复制到 apache2 配置目录。
<code>sudo mkdir /etc/apache2/ssl
sudo cp apache.pem /etc/apache2/ssl/apache.pem</code>
在 Windows 下貌似要进行下列的操作（直接使用 Apache msi 安装）：
<code>openssl req -new -out server.csr -config ..confopenssl.conf
openssl rsa -in privkey.pem -out server.key -config ..confopenssl.conf
openssl x509 -in server.csr -out server.crt -req -signkey server.key -days 999 -config ..confopenssl.conf</code>
复制的文件是 server.crt 和 server.key 到 conf 目录下。
完成后还需要修改虚拟主机设置。
<code>sudo nano /etc/apache2/sites-available/default</code>
修改 NameVirtualHost * 为：
<code>NameVirtualHost *:80
NameVirtualHost *:443</code>
然后增加新的虚拟主机配置文件。
<code>sudo mkdir -p /var/larryli
sudo nano /etc/apache2/sites-available/larryli</code>
内容如下：
<code>&lt;VirtualHost *:443&gt;
ServerSignature On
SSLEngine On
SSLCertificateFile /etc/apache2/ssl/apache.pem
ServerName larryli.vicp.net
ServerAdmin webmaster@localhost
DocumentRoot /var/larryli/
&lt;Directory /&gt;
Options FollowSymLinks
AllowOverride None
&lt;/Directory&gt;
&lt;Directory /var/larryli/&gt;
Options Indexes FollowSymLinks MultiViews
AllowOverride None
Order allow,deny
allow from all
&lt;/Directory&gt;
ErrorLog /var/log/apache2/larryli-error.log
LogLevel warn
CustomLog /var/log/apache2/larryli-access.log combined
&lt;/VirtualHost&gt;</code>
需要在 sites-enable 做一个符号链接才能启动该虚拟主机设置。
<code>sudo ln -s /etc/apache2/sites-available/larryli /etc/apache2/sites-enable/001-larryli</code>
001 是序数，以便 apache2 启动时按照正确的顺序加载配置
重新启动 apache2 即可使用 https 访问
<code>sudo /etc/init.d/apache2 restart</code>

然后安装 Subversion。
<code>sudo apt-get install subversion
sudo apt-get install libapache2-svn</code>
创建 svn 仓库。
<code>sudo svnadmin create /var/larryli</code>
因为要配置为通过 https 访问，更改文件属主。
<code>sudo chown -R www-data:www-data /var/larryli</code>
然后创建一个密码文件。
<code>sudo htpasswd -c /etc/subversion/passwd larryli</code>
（有文档写的是 htpassd2 命令）
可以增加多个用户。
然后修改虚拟主机配置文件。
<code>sudo nano /etc/apache2/sites-available/larryli</code>
内容如下：
<code>&lt;VirtualHost *:443&gt;
ServerSignature On
SSLEngine On
SSLCertificateFile /etc/apache2/ssl/apache.pem
ServerName larryli.vicp.net
ServerAdmin webmaster@localhost
&lt;Location /&gt;
DAV svn
SVNPath /var/larryli
AuthType Basic
AuthName "larryli subversion repository"
AuthUserFile /etc/subversion/passwd
&lt;LimitExcept GET PROPFIND OPTIONS REPORT&gt;
Require valid-user
&lt;/LimitExcept&gt;
&lt;/Location&gt;
ErrorLog /var/log/apache2/larryli-error.log
LogLevel warn
CustomLog /var/log/apache2/larryli-access.log combined
&lt;/VirtualHost&gt;</code>
上面的设置允许匿名用户访问 svn 库，但只允许认证用户提交修改。
如果不需要限制，将 LimitExcept 段代码全部删除即可。
如果要限制匿名用户访问，则删除  LimitExcept 但保留下面的代码：
<code>Require valid-user</code>
最后重新启动 Apache2。
<code>sudo /etc/init.d/apache2 restart</code>