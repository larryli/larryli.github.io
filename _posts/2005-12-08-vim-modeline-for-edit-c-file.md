---
ID: 262810
post_title: Vim modeline for edit C file
author: 南 靖男
post_date: 2005-12-08 20:49:29
post_excerpt: ""
layout: post
permalink: https://larryli.cn/2005/12/262810
published: true
---
<pre>/* {filename}.c: {descripion}
* Larry Li, {date} {copyright/copyleft}
* {date/version}: {modification}
* vi: set nu ts=4 sw=4 tw=72 :
* vim: set cin nocp is fo=tcqr cino=:0,p0,t0 :
* vim: set cinw=if,else,while,do,for,switch,case :
*/</pre>
以 vi: 开始的行用来设置编辑本 C 代码文本的属性。
nu 是 number 即在每一行文本前显示行号；
ts=4 设置 tabstop 即 Tab 字符所占的空格大小，默认是 8，但我一直以来都是用的 4，
8 个空格的大小实在太大，而 2、3 又太小，K&amp;R 好像也是用的 4 个空格缩进，所以选择了 4，
而直接将 tabstop 设置为 4 就可以不直接用 4 个 Space 而直接 1 个 Tab 来缩排了；
sw=4 就是 shiftwidth 用于缩排的空格数，自然是 4 了；
关于 ts 和 sw 的大小设置，Vm 手册中有专门的介绍：
<!--more-->
<blockquote>	3. Set 'tabstop' and 'shiftwidth' to whatever you prefer and use a
&amp;line;modeline&amp;line; to set these values when editing the file again.	Only
works when using Vim to edit the file.</blockquote>
所以我这里也就遵照建议使用了 modeline 来配置我的每一个 C 文件。
至于 tw=72 仅仅是一个参考，textwidth 可选的有 72 和 78 两个值，
古老的 stdout 们大多是 80 个字符的，78 个字符设置是考虑了两边显示附加列，
而 72 个字符设置自然是把打印/显示行号的地方也计算进去了。

以 vim: 开始的两行是控制 Vim 的 C 代码编辑行为。
cin cindent 打开 Vim 的 C 代码自动缩排功能；
nocp nocompatible 让 Vim 尽量的近似原始的 vi；
is incsearch 开启增量搜索；
fo=tcqr 设置 formatoptions 自动格式化信息：t 使用 textwidth 来自动换行，c 使用 textwidth 来自动换行注释文本，q 允许 gq 命令自动格式化注释行文本，r 允许换行后自动添加加注释行前导字符；
cino=:0,p0,t0 设置 cinoptions 缩排选项：:0 控制 switch 下行的缩进空格为 0，p0 控制 K&amp;R 函数参数说明缩进，t0 则控制返回类型的说明；
cinw=if,else,while,do,for,switch,case 是设置 cinwords 缩进关键字，除了 case 是回缩一个 shiftwidth 外，其他的都是前进一个 shiftwidth :)

实际上 ts=4 和 sw=4 是必要的外，其他的东东都可以不要。但是写上这长长的一串在代码之前却是一种别样的成就感，呵呵。