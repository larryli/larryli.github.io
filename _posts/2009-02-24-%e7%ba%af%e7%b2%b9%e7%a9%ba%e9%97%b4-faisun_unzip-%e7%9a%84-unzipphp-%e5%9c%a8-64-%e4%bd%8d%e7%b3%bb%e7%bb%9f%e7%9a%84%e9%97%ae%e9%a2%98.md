---
ID: 637121
post_title: >
  纯粹空间 Faisun_unzip 的 unzip.php
  在 64 位系统的问题
author: 南 靖男
post_date: 2009-02-24 20:35:44
post_excerpt: ""
layout: post
permalink: https://larryli.cn/2009/02/637121
published: true
---
<p>朋友反映在服务器上用不了这个 <a href="http://www.joomlagate.com/component/option,com_remository/Itemid,48/func,fileinfo/id,260/">unzip.php</a>，最近自己都是直接有 shell，就很少用这样的东东了。</p>  <p>因为朋友在本地环境中测试是好的，我也试了试，dump 了下数据，发现 zip 类下 ReadCentralDir 函数返回值不对。进而一步调试打印数据，就发现问题所在了。</p>  <p>服务器是 64 位系统，而本地是 32 位。所以 $bytes == 0x504b0506 的测试永远无法成功了。修改相关代码如下：</p> <code>$bytes=(($bytes &lt;&lt; 8 ) &amp; 0xffffffff) | ord($byte);</code>