---
ID: 384304
post_title: ANOS
author: 南 靖男
post_date: 2007-09-09 16:01:17
post_excerpt: ""
layout: page
permalink: https://larryli.cn/anos
published: true
---
<pre style="background-color: #000000"><font color="red">* <strong>ANOS: AN Operating System</strong>
* Released under the terms of BSD  Public Licence.
* Larry Li (<a href="mailto:tryos@126.com">tryos@126.com</a>), 2005</font>
<font color="#7f7fff"> Version: <a href="#v0.06">0.06</a> Released Time:  2005.3.29</font>
<font color="#ffffff"> Please waiting for next ANOS...</font></pre>
<img src="https://larryli.cn/wp-content/uploads/50/5051/2007/09/logo.bmp" alt="ANOS Logo" />

<strong>ANOS 介绍：</strong>
<ul>ANOS 是一个操作系统(AN Operating System)。一个尽可能简单的 i386  操作系统，或者说仅仅只是一个系统。不需要其他东东就可以在电脑中运行的程序。
ANOS 本身不是为了作为一个实用的 OS 而存在，而是为了作为一个 OS  演示而存在。尽可能简单的展示一个操作系统的具体代码就是 ANOS 的目的。虽然 <a href="http://www.cs.vu.nl/%7East/minix.html" target="_blank">Minix</a> 还有 <a href="http://www.oldlinux.org/" target="_blank">Linux 0.01/0.11</a> 同样为我们提供这样的演示。但是  Minix 基于微内核以及完成很多额外工作(这是一个实用的系统所必须的)，其代码还是相当庞大的。至于 Linux  初始版本，当然是研究一个小系统的好例子，但其代码有点混乱(很强的黑客风格)。而其他的小 OS  不是未完成就是有着这样那样的弊端。
弊端其中之一就是，我们当前多半使用的是 Win32 系统，而这些小 OS 很少是在 Win32  平台下开发的。仅仅靠阅读代码也无法了解 OS 的，所以研究起这些 OS  来缺少一个实际动手的机会。往往大家只是构筑一个研究用的平台就烦的撒手不干了。
所以，ANOS 选用 Win32 下 MinGW GNU C 编译器和  NASM 汇编器以及 QEMU 模拟器来进行开发。同时，ANOS 会根据进度发布一个 OS 在不同阶段的源代码包，展示 OS  开发中状态。并且尽可能的提供足够的文档资料以及代码注释。方便大家自己动手参与进 ANOS 的代码，了解 OS。</ul>
<strong>开发记录：</strong>
<ul>
	<li><a title="v0.06" name="v0.06"></a>2005.3.29  v0.06
整理所有字符串信息(info.c,info.h)
添加内核命令行(kshell.c,kshell.h)
内核命令行行程编辑(kgetline.h)
内核命令计算器(ksiac.h)
<a href="http://gro.clinux.org/frs/download.php/976/anos.0.06.tgz">http://gro.clinux.org/frs/download.php/976/anos.0.06.tgz</a></li>
	<li><a title="v0.05" name="v0.05"></a>2005.3.23  v0.05
添加键盘按键定义(key.h)
添加键盘映射表处理(keymap.c,keymap.h)
添加美式键盘映射表(keymapus.h)
添加日式键盘映射表(keymapjp.h)
添加键盘驱动(kbd.c,kbd.h)
修正  <a href="#v0.03">v0.03 FIXME</a>(start.asm)
<a href="http://gro.clinux.org/frs/download.php/974/anos.0.05.tgz">http://gro.clinux.org/frs/download.php/974/anos.0.05.tgz</a></li>
	<li><a title="v0.04" name="v0.04"></a>2005.3.22 v0.04
添加硬件中断处理(irq.c,irq_s.asm,irq.h)
添加  CMOS 信息定义(cmos.h)
添加系统时钟驱动(time.c,time.h)
<a href="http://gro.clinux.org/frs/download.php/970/anos.0.04.tgz">http://gro.clinux.org/frs/download.php/970/anos.0.04.tgz</a></li>
	<li><a title="v0.03" name="v0.03"></a>2005.3.21  v0.03
添加系统蓝屏错误输出(panic.c,panic.h)
添加中断服务处理(isr.c,isc.h)
添加系统异常处理(traps.c,traps_s.asm,traps.h)
FIXME:  traps_s.asm 中 pop es 会产生 13, General Protection Fault 异常
<a href="http://gro.clinux.org/frs/download.php/969/anos.0.03.tgz">http://gro.clinux.org/frs/download.php/968/anos.0.03.tgz</a></li>
	<li><a title="v0.02" name="v0.02"></a>2005.3.19 v0.02
添加 ANOS 全局定义(anos.h)
添加基本支持 C  库(misc.c,misc.h)
添加硬件基本输入输出操作(io.h)
添加 VGA 03h 80x25 16  色字符模式显示(vga.c,vga.h)
<a href="http://gro.clinux.org/frs/download.php/966/anos.0.02.tgz">http://gro.clinux.org/frs/download.php/966/anos.0.02.tgz</a></li>
	<li><a title="v0.01" name="v0.01"></a>2005.3.1  v0.01
完成软盘映象制作(fdmake.c)
完成启动代码(boot.asm)，进入保护模式(start.asm)，C  程序链接(main.c)
<a href="http://gro.clinux.org/frs/download.php/957/anos.0.01.tgz">http://gro.clinux.org/frs/download.php/957/anos.0.01.tgz</a></li>
</ul>
<strong>硬件需求：</strong>
<ul>IBM 及其兼容 PC，80486 DX 以上 CPU，20M 内存，100 M 硬盘空间(偶的破本本..)</ul>
<strong>软件需求：</strong>
<ul>ReactOS, Windows 9x/ME/NT/2000/XP/2003
MinGW 3.1.0-1 建议 gcc 使用 3.3.1  以上版本
NASM 0.98.35(不能使用 0.98 版)
QEMU 0.5.5
GNU tar 1.13.19(不必须)
gzip  1.2.4(不必须)</ul>
<strong>历史注记：</strong>
<ul>2002 年开始接触 chinaos 就是 <a href="http://asmcos.51.net/" target="_blank">http://asmcos.51.net</a> 关注 cnix 的开发、讨论 MINIX  系统，结识了不少朋友，学到了很多。到年底的时候认识了 sunwen，因为同样喜欢上武汉自由软件协会论坛(<a href="http://www.clinux.org/forum" target="_blank">http://www.clinux.org/forum</a>)的关系，帮他在 GRO (<a href="http://gro.clinux.org/" target="_blank">http://gro.clinux.org</a>)做了一个 OS  开发讲座。后来，就加入了他的 Lingix (<a href="http://lingix.gro.clinux.org/" target="_blank">http://lingix.gro.clinux.org</a>)开发，做一些简单的工作。2003 年夏天(其实更早)，Lingix  就完全停止了。其中原因有很多(比如 ANOS 的 fdmake 工具就是那时候计划做的而没做，还有用 MinGW 编译器替换 DJGPP  的工作)，我个人方面的就是我的懒惰。工作上的原因一直拖到 2004 年底(其间有过 <a href="http://www.reactos.com/" target="_blank">ReactOS</a> 的汉化，终究没有人参与，一人力不从心而放弃；又有 <a href="http://www.mimios.com/" target="_blank">mimios</a> 的讲座，突然一下就结束了)，心里还是有想做完一个小  OS 的期盼。随后就开始 Try OS 的设计，也就是现在的 ANOS。而真正动手，则已是 2005 年春天，Lingix 结束整整两年后。</ul>
<strong>联系我：</strong>
<ul>电子邮件：<a href="mailto:tryos@126.com" target="_blank">tryos@126.com</a>
项目主页：<a href="https://larryli.cn/anos" target="_blank">https://larryli.cn/anos</a>
代码发布：<a href="http://gro.clinux.org/frs/?group_id=241" target="_blank">http://gro.clinux.org/frs/?group_id=241</a>
开发论坛：<a href="http://www.reactoschina.com/forum/viewforum.php?f=1" target="_blank">http://www.reactoschina.com/forum</a></ul>