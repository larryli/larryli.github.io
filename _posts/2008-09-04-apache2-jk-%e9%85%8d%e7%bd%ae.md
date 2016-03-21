---
ID: 630877
post_title: Apache2 jk 配置
author: 南 靖男
post_date: 2008-09-04 10:25:31
post_excerpt: ""
layout: post
permalink: https://larryli.cn/2008/09/630877
published: true
---
因为不是每个应用都需要使用 jk 转发到 Tomcat 所以修改了下加载。
首先当前的 Ubuntu Server 似乎把 jk.conf 直接丢在 /etc/apache2/conf.d 下，而不是放在 /etc/apache2/mods-available 目录。
自然使用 sudo a2enmod jk 的时候就不会创建 /etc/apache2/mods-enabled/jk.conf 软连接。
所以先要把这个文件移到 /etc/apache2/mods-available：
<code>sudo mv /etc/apache2/conf.d/jk.conf /etc/apache2/mods-available</code>
修改 /etc/apache2/mods-available/jk.conf 内容如下：
<code>JkWorkersFile /etc/libapache2-mod-jk/workers.properties
# Where to put jk logs
JkLogFile /var/log/apache2/mod_jk.log
# Set the jk log level [debug/error/info]
JkLogLevel info
# Select the log format
JkLogStampFormat "[%a %b %d %H:%M:%S %Y]"
# JkOptions indicate to send SSL KEY SIZE,
JkOptions +ForwardKeySize +ForwardURICompat -ForwardDirectories
# JkRequestLogFormat set the request format
JkRequestLogFormat "%w %V %T"
# 将所有servlet 和jsp请求通过ajp13的协议送给Tomcat，让Tomcat来处理
#JkMount /servlet/* ajp13_worker
#JkMount /*.jsp ajp13_worker
#JkMount /*.do ajp13_worker
JkShmFile /var/log/jk-runtime-status
#&lt;LocationMatch .*web-inf.*=""&gt;
#       AllowOverride None
#       deny from all
#&lt;/LocationMatch&gt;</code>
也就是注释掉 JkMount 设置和 LocationMatch 节。
如果已经启动 jk 模块，需要自行创建一个软连接：
<code>sudo ln -s /etc/apache2/mods-available/jk.conf /etc/apache2/mods-enabled/jk.conf</code>
没有启用，直接使用 sudo a2enmod jk 即可。
然后创建一个 mods-optional 用来放置可选的模块配置文件。
<code>sudo nano /etc/apache2/mods-optional/jk.conf</code>
内容如下：
<code>&lt;IfModule mod_jk.c&gt;
# 将所有servlet 和jsp请求通过ajp13的协议送给Tomcat，让Tomcat来处理
#JkMount /servlet/* ajp13_worker
JkMount /*.jsp ajp13_worker
JkMount /*.do ajp13_worker
&lt;LocationMatch '.*WEB-INF.*'&gt;
#&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; AllowOverride None
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; deny from all
&lt;/LocationMatch&gt;
&lt;/IfModule&gt;</code>
也就是在 /etc/apache2/mods-available/jk.conf 注释掉的内容，并且加上了 IfModule mod_jk.c 判断。
最后就是在虚拟主机的配置文件中 Include：
<code>sudo nano /etc/apache2/sites-available/test</code>
示例内容如下：
<code>&lt;VirtualHost *:80&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Servername www.test.com
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ServerAdmin webmaster@test.com
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; DocumentRoot /var/www/jsp/test
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; DirectoryIndex index.html index.htm index.jsp
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;Directory /&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Options FollowSymLinks
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; AllowOverride None
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;/Directory&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;Directory /var/www/jsp/test&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Options FollowSymLinks MultiViews
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; AllowOverride None
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Order allow,deny
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; allow from all
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;/Directory&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Include /etc/apache2/mods-optional/jk.conf
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ErrorLog /var/log/apache2/error.test.log
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; # Possible values include: debug, info, notice, warn, error, crit,
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; # alert, emerg.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; LogLevel warn
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; CustomLog /var/log/apache2/access.test.log combined
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ServerSignature On
&lt;/VirtualHost&gt;</code>
一点题外话：最近配置 tomcat 虚拟主机的时候总是处理不了 *.do 转发，原因是一直以来都是将虚拟主机的 appBase 目录和应用的 docBase 目录放在同一目录下。
也就是 appBase 直接指向程序，docBase 为 . 当前目录。实际上这种配置不能完全满足需要。
修改 server.xml 相关部分如下：
<code>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;Host name="www.test.com" debug="0"
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; appBase="/var/www/jsp" unpackWARs="false"
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; autoDeploy="false" xmlValidation="false" xmlNamespaceAware="false"&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;Context path="" docBase="test" /&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;Logger className="org.apache.catalina.logger.FileLogger"
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; directory="logs"
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; prefix="test_log." suffix=".txt" timestamp="true" /&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;/Host&gt;</code><div class="flockcredit" style="text-align: right; color: #CCC; font-size: x-small;">用 <a href="http://www.flock.com/blogged-with-flock" style="color: #999; font-weight: bold;" target="_new" title="Flock Browser">Flock 浏览器</a> 创建</div>