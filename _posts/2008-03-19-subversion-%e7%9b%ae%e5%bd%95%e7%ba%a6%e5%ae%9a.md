---
ID: 625162
post_title: Subversion 目录约定
author: 南 靖男
post_date: 2008-03-19 11:46:14
post_excerpt: ""
layout: post
permalink: https://larryli.cn/2008/03/625162
published: true
---
svn 的分支处理与 cvs 不同，cvs 是采用内置命令生产新的内部结构来存放分支差异，而 svn 则是由用户自己来设计。
一般来说，svn 仓库下约定有三个目录：trunk、branches 和 tags，分别存放主干、分支和标记。
trunk 直接存放主干源代码，branches 和 tags 下会有二级目录，其目录名就是分支和标记名。
当然，根据项目人员的喜好，在 branches 和 tags 下使用多层目录也是可以，比如专门的 tags/release 下在标记出 1.0 发布版本，而 tags/test 下的 1.0 则是内部测试版。而对于 1.0 测试版本的补丁修改则放到 branches/test/1.0 下。
另外，如果一个仓库存放多个项目可以采用 prjname/trunk、prjname/branches、prjname/tags 的目录划分；或者 trunk/prj1、trunk/prj2、branches/prj1/release1、branches/prj2/release1 之类的目录划分。
总之，svn 的分支目录只是一种约定。