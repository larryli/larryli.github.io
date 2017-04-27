---
ID: 632219
post_title: >
  设置 Google 浏览器 Chrome 的 Gmail
  应用程序作为 Windows
  系统的默认邮件客户端
author: 南 靖男
post_date: 2008-11-03 11:26:46
post_excerpt: ""
layout: post
permalink: 2008/11/632219
published: true
---
<a href="http://www.google.com/chrome">Google 浏览器 Chrome</a> 可以将网站应用创建为独立的应用程序，比如 GMail。可以将该程序直接设置为 Windows 默认的邮件处理程序。
新建一个文件，修改文件名为 gmail.reg 内容如下：

<code>Windows Registry Editor Version 5.00
[HKEY_LOCAL_MACHINESOFTWAREClientsMailGoogle Mail]
@="Google Mail"
[HKEY_LOCAL_MACHINESOFTWAREClientsMailGoogle Mailshell]
[HKEY_LOCAL_MACHINESOFTWAREClientsMailGoogle Mailshellopen]
@="Google Mail"
[HKEY_LOCAL_MACHINESOFTWAREClientsMailGoogle Mailshellopencommand]
@=""C:\Documents and Settings\larry\Local Settings\Application Data\Google\Chrome\Application\chrome.exe" --app=https://mail.google.com/mail"
[HKEY_LOCAL_MACHINESOFTWAREClientsMailGoogle MailDefaultIcon]
@="C:\DOCUME~1\larry\LOCALS~1\APPLIC~1\Google\Chrome\USERDA~1\Default\PLUGIN~1\GOOGLE~1\mail.google.com\https_443\icons#desktop\Gmail.ico"</code>   

command 和 DefaultIcon 的值可以参考 Chrome 创建的 GMail 应用程序的值。<!--more-->
在快捷方式上右键点击，属性：目标就是 command，更改图标就是 DefaultIcon
需要注意到是引号和反斜杠前面必须再加一个反斜杠。

保存文件，双击导入到系统。然后在 IE 选项、程序中设置默认的邮件应用程序为 Google Mail。
对于 Windows XP 开始菜单上显示的邮件客户端，也可以开始菜单自定义中选择。

<div class="flockcredit" style="text-align: right; color: #CCC; font-size: x-small;">用 <a href="http://www.flock.com/blogged-with-flock" style="color: #999; font-weight: bold;" target="_new" title="Flock Browser">Flock 浏览器</a> 创建</div>