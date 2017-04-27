---
ID: 643502
post_title: jQuery 实现：豆瓣小组显示楼层
author: 南 靖男
post_date: 2009-11-21 12:59:05
post_excerpt: ""
layout: post
permalink: 2009/11/643502
published: true
---
<p>右键将这个“<a href="javascript:void((function(){var%20start=1,mts=/%5C?.*start=(%5Cd+)/i.exec(window.location.href);if(mts!=null)start+=parseInt(mts[1]);$(%27li.clearfix%20&gt;%20div.reply-doc%20h4%27).each(function(i){$(this).filter(%27:not(:has(div))%27).prepend(%27&lt;div%20style=&quot;float:right;&quot;&gt;#%27+(start+i)+%27&lt;/div&gt;%27)})})())" title="显示楼层">显示楼层</a>”加入收藏夹/书签，然后在豆瓣的小组话题页面点击这个书签，就可以了。</p>
<p>源代码：<br />
<code>var start = 1, mts = /?.*start=(d+)/i.exec(window.location.href);<br />
if (mts != null)<br />
start += parseInt(mts[1]);<br />
$('li.clearfix &gt; div.reply-doc h4').each(function (i) {<br />
$(this).filter(':not(:has(div))').prepend('&lt;div style="float: right;"&gt;#' + (start + i) +'&lt;/div&gt;');<br />
})</code></p>
<div class="flockcredit" style="text-align: right; color: #CCC; font-size: x-small;">用 <a href="http://www.flock.com/blogged-with-flock" style="color: #999; font-weight: bold;" target="_new" title="Flock 浏览器">Flock 浏览器</a> 创建</div>