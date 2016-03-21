---
ID: 630572
post_title: Ubuntu 远程登录中文语言设置
author: 南 靖男
post_date: 2008-08-22 13:25:39
post_excerpt: ""
layout: post
permalink: https://larryli.cn/2008/08/630572
published: true
---
因为默认会在控制台操作，所以安装 Ubuntu Server 的时候选择的还是英文，而不是中文。但是用 PuTTY 远程登录的时候，能显示命令的中文界面未尝不是件好事。
首先，看一下是否激活了 zh_CN.UTF-8 locale 设置。下面的命令：
<code>cat /var/lib/locales/supported.d/local</code>
如果没显示 zh_CN.UTF-8 UTF-8 可以直接编辑这个文件，加上这一行。当然可以执行命令：
<code>sudo locale-gen zh_CN.UTF-8</code>
建议完成后再配置一下 locale：
<code>sudo dpkg-reconfigure locales</code>
然后就是安装语言包了：
<code>sudo apt-get install manpages-zh language-pack-zh</code>
最后当然是设置一下 LANG 和 LANGUAGE 环境变量，可以在 PuTTY 中设置，也可以修改自己的 .profile
<code>nano ~/.profile</code>
在最后加上：
<code>export LANG=zh_CN.UTF-8
export LANGUAGE=zh_CN:zh</code>


   <div class="flockcredit" style="text-align: right; color: #CCC; font-size: x-small;">用 <a href="http://www.flock.com/blogged-with-flock" style="color: #999; font-weight: bold;" target="_new" title="Flock Browser">Flock 浏览器</a> 创建</div>