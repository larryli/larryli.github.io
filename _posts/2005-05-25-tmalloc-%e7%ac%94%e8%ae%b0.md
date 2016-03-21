---
ID: 262689
post_title: TMalloc 笔记
author: 南 靖男
post_date: 2005-05-25 21:30:33
post_excerpt: ""
layout: post
permalink: https://larryli.cn/2005/05/262689
published: true
---
<a href="http://www.john.findlay1.btinternet.co.uk">John Findlay</a> 的 TMalloc Lib 是用于查错调试，而不是用于产品。
昨天大致看了下代码，就发现需要自己添加一些些东西。
今天仔细瞧瞧，看见那个 alloc memory 块前的双向链表，就在想是不是使用 Hash 来，效率更高一些。等到看完所有实现，才知道 List 是最好的。因为 TMalloc 考虑了偏移。如果操作的不是直接分配内存块，而是偏移，要找到这个偏移原本的记录头，只能遍历整个链表。
所以说，TMalloc 的实现很缺乏效率。但是能够保证发现问题。
话说回来，依我的想法，在考虑效率的产品级实现里面，应该可以自己先分配大块内存，使用自己来管理内存分配。这样在分配程序从系统申请的有限大块内存间使用双向链表遍历。而内存管理里面可以直接使用偏移进行二分查找来定位程序使用的内存块。。。
不管怎么样，内存保护/回收处理都是牺牲效率的冗长代码。我的 malloc lib 还是基于 K&amp;P 的 EMalloc 的简单扩展算了。