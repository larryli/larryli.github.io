---
ID: 634538
post_title: >
  Subversion post-commit
  钩子：监视提交路径自动更新代码
author: 南 靖男
post_date: 2008-12-04 23:10:59
post_excerpt: ""
layout: post
permalink: 2008/12/634538
published: true
---
<code>#!/bin/sh
# 配置库地址
REPOS="$1"
REV="$2"
# 监视的路径
REPOSPATH=branches/release
# 要自动 update 的实际路径
REALPATH=/var/www
# svn 相关命令
SVN=/usr/bin/svn
SVNLOOK=/usr/bin/svnlook
GREP=/bin/grep
export LANG="zh_CN.UTF-8"
if ($SVNLOOK dirs-changed $REPOS | $GREP "^$REPOSPATH/" &gt; /dev/null) then
  $SVN update $REALPATH
fi</code>
开发代码工作在 trunk 上，测试的时候复制到 tags/test-xxyyzz。如果要发布再复制到 tags/release-xxyyzz，然后在合并到 branches/release。利用这个脚本就在服务器上自动更新代码发布。<div class="flockcredit" style="text-align: right; color: #CCC; font-size: x-small;">用 <a href="http://www.flock.com/blogged-with-flock" style="color: #999; font-weight: bold;" target="_new" title="Flock Browser">Flock 浏览器</a> 创建</div>