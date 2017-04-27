---
ID: 645625
post_title: '使用 Caddy 和 Dnspod 自动申请 Let&#8217;s Encrypt 证书'
author: 南 靖男
post_date: 2017-04-27 14:31:19
post_excerpt: ""
layout: post
permalink: https://larryli.cn/2017/04/645625
published: true
---
<a href="https://letsencrypt.org/">Let's Encrypt</a> 申请证书的 <a href="https://ietf-wg-acme.github.io/acme/">ACME 协议</a>支持三种认证，分别是：
<ol>
 	<li>基于 80 端口的 http-01</li>
 	<li>基于 443 端口的 tls-sni-02</li>
 	<li>无需端口的 dns-01</li>
</ol>
<code>dns-01</code> 需要在 DNS 服务器增加对应的 TXT 记录来完成验证。

<a href="http://caddyserver.com">Caddy</a> 现在有官方的 <a href="https://caddyserver.com/docs/tls.dns.dnspod">tls.dns.dnspod</a> 插件支持托管在 <a href="https://www.dnspod.cn/">Dnspod</a> 的域名使用 <code>dns-01</code> 来申请 Let's Encrypt 证书。

首先，需要在 Dnspod <a href="https://www.dnspod.cn/console/user/security">用户中心的安全设置</a>中申请 API Token，复制其 ID 和 TOKEN。

然后，修改 Caddy 服务配置脚本，比如 sysvinit 系统的 <code>/etc/init.d/caddy</code> 在 <code>export CADDYPATH=/etc/ssl/caddy</code> 后面增加一行：

<code>
export DNSPOD_API_KEY="$ID,$TOKEN"
</code>

就是用 ID 和 TOKEN 以英文逗号分割的字符串。

最后，就是在对应的 Caddyfile 文件配置中启用：

<code>
tls {
    dns dnspod
}
</code>

如果有配置多个域名，第一次启动会比较缓慢。因为需要每个域名依次申请证书。

题外话：
<ul>
	<li>树莓派 1 代在<a href="https://caddyserver.com/download">下载 Caddy</a> 时需要在 PLATFORM 选择 Linux ARMv6，然后在 PLUGINS 中选择 tls.dns.dnspod 即可。</li>
	<li>如果 Dnspod 自己支持 DDNS 接口，不过一般路由器比如 TP-LINK 系都会支持花生壳 DDNS，自动在路由连接时登记，比定时脚本要靠谱很多。自己的域名只需要在 Dnspod 中 CNAME 到花生壳的免费域名。</li>
	<li>一般情况，运营商不会开放 80 端口，但 443 端口是开放的。只需要在路由器将 443 端口转发给内网设备。</li>
	<li>Caddy 可以作为前端反向代理系统的其他的 http 服务，只需要每个服务多建一个域名即可。</li>
</ul>