---
ID: 262771
post_title: 使用 Tor + Privoxy + Firefox
author: 南 靖男
post_date: 2005-10-28 20:35:47
post_excerpt: ""
layout: post
permalink: https://larryli.cn/2005/10/262771
published: true
---
我真的不想写下面的文字，但是既然有 Great Firewall，那么 Tor 的出现也是应该！
不要问我下面到底在做什么，我只能说我爱维基，我是维基人。
与政治无干，只是为了 <strong>Free As In Freedom</strong> 的 GNU 精神。
<!--more-->

首先下载 <a href="http://tor.eff.org:80/dist/win32/tor-0.1.1.2-alpha-win32.exe">Tor</a>
Tor 安装好后直接运行就可以了（如果不想看见那个黑黑的命令行提示符请看本文最下面），正常的话应该显示当前版本和 Success 信息，并且 Looks like it's working。
但是 Tor 只支持 FTP 和 Socket 的匿名代理，并不支持 HTTP 也就是网页浏览的代理。

所以接着是 <a href="http://kent.dl.sourceforge.net:80/sourceforge/ijbswa/privoxy_setup_3_0_3-2.exe">Privoxy</a>
Privoxy 需要配置以配合 Tor 来工作，运行 Privoxy 在 Options 菜单 Edit Main Configuration。
这时，Privoxy 会调用文本编辑器打开配置文本，找到 5.2. forward-socks4 and forward-socks4a 项目。
配置文件中以 # 开头的行为注释，这里有相当部分关于 forward-socks 的注释，如果看的懂英文的话仔细看看比较好。
看不懂的，找一个空行，输入 <font color="#ff0000"><code>forward-socks4a / localhost:9050 .</code></font> 注意最后一个点点，不要掉了。
然后最好关闭 Privoxy 的日志功能，找到 <font color="#ff0000"><code>logfile privoxy.log</code></font> 和 <font color="#ff0000"><code>jarfile jar.log</code></font> 两行，前面加上 <font color="#ff0000"><code>#</code></font> 注释掉，关闭日志。
编辑完了，保存。并且选择 Exit Privoxy 退出 Privoxy 后再重新启动它。

然后下载安装 Firefox（略过，呵呵）。在 Firefox “工具”菜单“选项”对话框“基本信息”右下“连接设置”对话框选择“手动配置代理”，将“HTTP 代理设置”为 <font color="#ff0000">localhost</font>，端口是 Privoxy 的服务端口 <font color="#ff0000">8118</font>。至于“FTP 代理”和“SOCKS 代理”也是 <font color="#ff0000">localhost</font>，但是端口可以直接是 Tor 的服务端口 <font color="#ff0000">9050</font>。然后下面选定“SOCKS v5”就 OK 了。

Privoxy 最小化就可以在任务栏图标了，至于中间显示的信息可以去掉 View 菜单里面的勾勾即可。
而让 Tor 隐藏运行，只能把它当作服务进程自动运行，按以下步骤：
一、将你的系统盘 C:Documents and Settings你的用户名Application DataTorTorrc 文件复制至 Tor 安装目录下。
二、打开命令提示符，进入 Tor 所在目录，运行 tor -install 命令即可。Tor 会在系统中添加一个 Tor Win32 Service 的系统服务，并自动启动。如果想取消自动运行，进入所在目录，运行 tor -remove 命令即可。