---
ID: 644823
post_title: Ubuntu Server 14.04 使用 Ruby 2.0
author: 南 靖男
post_date: 2014-05-14 14:26:12
post_excerpt: ""
layout: post
permalink: https://larryli.cn/2014/05/644823
published: true
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:1122:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    </pre></td><td class="code"><pre class="sh" style="font-family:monospace;">sudo rm /usr/bin/ruby /usr/bin/gem /usr/bin/irb /usr/bin/rdoc /usr/bin/erb
    sudo ln -s /usr/bin/ruby2.0 /usr/bin/ruby
    sudo ln -s /usr/bin/gem2.0 /usr/bin/gem
    sudo ln -s /usr/bin/irb2.0 /usr/bin/irb
    sudo ln -s /usr/bin/rdoc2.0 /usr/bin/rdoc
    sudo ln -s /usr/bin/erb2.0 /usr/bin/erb
    sudo gem sources --remove https://rubygems.org/
    sudo gem sources -a https://ruby.taobao.org/
    sudo gem update --system
    sudo gem pristine --all</pre></td></tr></table><p class="theCode" style="display:none;">sudo rm /usr/bin/ruby /usr/bin/gem /usr/bin/irb /usr/bin/rdoc /usr/bin/erb
    sudo ln -s /usr/bin/ruby2.0 /usr/bin/ruby
    sudo ln -s /usr/bin/gem2.0 /usr/bin/gem
    sudo ln -s /usr/bin/irb2.0 /usr/bin/irb
    sudo ln -s /usr/bin/rdoc2.0 /usr/bin/rdoc
    sudo ln -s /usr/bin/erb2.0 /usr/bin/erb
    sudo gem sources --remove https://rubygems.org/
    sudo gem sources -a https://ruby.taobao.org/
    sudo gem update --system
    sudo gem pristine --all</p></div>
    ";}
---
官方源已经提供了 ruby2.0 但是因为 debian 源<a href="https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=737782">处理 bug</a> <a href="https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=741050">删除了 ruby-switch 包</a>，就<a href="http://askubuntu.com/questions/452243/what-versions-of-ruby-are-supported-in-14-04">无法使用 update-alternatives 来切换 ruby 版本</a>了。

目前就只有<a href="http://blog.costan.us/2014/04/restoring-ruby-20-on-ubuntu-1404.html">手工切换</a>一下，命令如下：
<pre lang="SH" line="1">sudo rm /usr/bin/ruby /usr/bin/gem /usr/bin/irb /usr/bin/rdoc /usr/bin/erb
sudo ln -s /usr/bin/ruby2.0 /usr/bin/ruby
sudo ln -s /usr/bin/gem2.0 /usr/bin/gem
sudo ln -s /usr/bin/irb2.0 /usr/bin/irb
sudo ln -s /usr/bin/rdoc2.0 /usr/bin/rdoc
sudo ln -s /usr/bin/erb2.0 /usr/bin/erb
sudo gem sources --remove https://rubygems.org/
sudo gem sources -a https://ruby.taobao.org/
sudo gem update --system
sudo gem pristine --all</pre>

嗯，顺便把 rubygems 切换到<a href="https://ruby.taobao.org/">淘宝镜像</a>。不知道什么时候 <a href="https://packagist.org/">packagist</a> 也有国内镜像啊；每次本地 composer update 都是在消耗时间。