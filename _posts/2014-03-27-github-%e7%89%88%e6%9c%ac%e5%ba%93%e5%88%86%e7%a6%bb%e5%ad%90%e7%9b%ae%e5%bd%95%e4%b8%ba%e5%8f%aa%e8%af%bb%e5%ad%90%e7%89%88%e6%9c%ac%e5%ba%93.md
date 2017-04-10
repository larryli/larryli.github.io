---
ID: 644804
post_title: >
  github
  版本库分离子目录为只读子版本库
author: 南 靖男
post_date: 2014-03-27 15:11:36
post_excerpt: ""
layout: post
permalink: https://larryli.cn/2014/03/644804
published: true
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:343:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    </pre></td><td class="code"><pre class="sh" style="font-family:monospace;">git subsplit init https://github.com/yourname/foo</pre></td></tr></table><p class="theCode" style="display:none;">git subsplit init https://github.com/yourname/foo</p></div>
    ;i:2;s:283:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    </pre></td><td class="code"><pre class="sh" style="font-family:monospace;">git subsplit update</pre></td></tr></table><p class="theCode" style="display:none;">git subsplit update</p></div>
    ;i:3;s:395:
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    </pre></td><td class="code"><pre class="sh" style="font-family:monospace;">git subsplit publish bar:https://github.com/yourname/foo-bar --heads=master</pre></td></tr></table><p class="theCode" style="display:none;">git subsplit publish bar:https://github.com/yourname/foo-bar --heads=master</p></div>
    ";}
---
Github 的官方文档有说明<a href="https://help.github.com/articles/splitting-a-subpath-out-into-a-new-repository" title="Splitting a subpath out into a new repository" target="_blank">如何使用 git 分离一个已存在版本库的子目录到新的版本库</a>。但这玩意就是一次性的。分离之后，父库上的子目录修改没办法自动同步到子库上。

幸好 github 上也有人提供了同步工具 <a href="https://github.com/dflydev/git-subsplit" title="Automate and simplify the process of managing one-way read-only subtree splits." target="_blank">git-subsplit</a>。

使用起来很简单。

首先，你得至少有两个版本库。比如在 github 分别是 https://github.com/yourname/foo 和 https://github.com/yourname/foo-bar 其中，foo-bar 对应 foo/bar 目录。foo-bar 最好是空仓库。

然后检出 foo 到本地，创建 foo/bar 目录，增加点内容。

可以在 foo 本地目录，也可以另找一个地方，执行：
<pre lang="SH" line="1">git subsplit init https://github.com/yourname/foo</pre>
设置父版本库。这个只需要一次执行。

等到父版本库有新的 push/pull 后，回到该目录下，执行：
<pre lang="SH" line="1">git subsplit update</pre>
更新（pull）父版本库的变更。

最后，执行：
<pre lang="SH" line="1">git subsplit publish bar:https://github.com/yourname/foo-bar --heads=master</pre>
同步变更到子版本库。子目录可以多层，也可以同步多个。