---
layout: post
title:  版本管理工具的前世今生, Kannel, awk&sed&grep, Win10历险记
category: linux 
---

# 版本管理工具的前世今生

参考Wiki的相关词条，可将版本工具分为三代：

1.本地版本管理

开源：SCCS (1972) RCS (1982)

私有：PVCS (1985) QVCS (1991)

以RCS最为著名，不过由于年代久远，我从来没用过。

2.客户端/服务器版本管理

开源：CVS (1986, 1990 in C) CVSNT (1998) QVCS Enterprise (1998) Subversion (2000)

私有：Software Change Manager (1970s) Panvalet (1970s) Endevor (1980s) DSEE (1984) Synergy (1990) ClearCase (1992) CMVC (1994) Visual SourceSafe (1994) Perforce (1995) StarTeam (1995) Integrity (2001) Surround SCM (2002) AccuRev SCM (2002) SourceAnywhere (2003) Vault (2003) Team Foundation Server (2005) Team Concert (2008)

我用过的包括CVS、SVN、ClearCase和Visual SourceSafe。

这一代的工具，以CVS为开端。ClearCase和Visual SourceSafe与CVS差不多同时期，因此功能上也多有相同，总的来说就是ClearCase功能强，但不好用。SourceSafe好用，但功能差。

其中，ClearCase我在之前的公司有用过，当时为了简单的check in和check out，竟然还需要编写脚本以简化流程。不过功能的确是没的说，分支合并权限都不在话下。

VSS以现在的角度来看，基本就是个垃圾了，它是MS收购的一家公司的产品，目的是填补VS在这方面的空白。但这样弱的工具，即使MS内部的人也基本不用，这也是后来MS发布Team Foundation Server的重要原因。

SVN是这一代的集大成者，使用简单的同时，仍保有相当强度的功能，唯一诟病的就是合并功能太弱。

3.分布式版本管理

开源：GNU arch (2001) Darcs (2002) DCVS (2002) ArX (2003) Monotone (2003) SVK (2003) Codeville (2005) Bazaar (2005) Git (2005) Mercurial (2005) Fossil (2007) Veracity (2010)

私有：TeamWare (1990s?) Code Co-op (1997) BitKeeper (1998) Plastic SCM (2006)

早期比较有名的是BitKeeper。它在2002~2005年是Linux Kernel所使用的版本工具。Linus曾经非常喜欢它。可惜后来由于商业利益的关系，开发者的要挟惹毛了Linus。大神发威开发了Git，从此BitKeeper也就无人问津了。

从这件事情可以看出，Linus其实并不是一个像Richard Stallman那样的开源洁癖狂，现有的东西够用，他就懒得节外生枝了。但也不要因此小看他的水平，大神发起威来，搞死像BitKeeper这样的工具还是绰绰有余的。

目前较为主流的Bazaar、Git和Mercurial都出现在2005年，这并不是偶然的。实际上都是BitKeeper和开源社区之间战争的产物。

后Git时代的工具，如Fossil和Veracity，相比Git来说，对权限、BUG跟踪之类的功能做了进一步的扩展。

# Kannel

Kannel是一个开源的WAP&SMS网关项目。

官网：

http://www.kannel.org/

这里提到这个项目，并非它有多么重要——实际上它从2010年之后就几乎没有更新了，最新的版本定格在2014年。它所代表的WAP已经无人问津，至于SMS吧，似乎又用不到这么复杂的框架。

但我之所以要提它，主要在于情怀。2007年底的时候，公司给我安排了一个在App中集成彩信发送功能的任务。当时由于能力尚浅，虽然努力了一个月，最终却没有实际成果，很是让领导质疑了一阵，幸好接手的哥们同样做不出来，而我的下一个任务——使用jpeglib，获得了成功，才算将事情平息下来。

过了一年，闲暇无聊之际，旧事重提，于是发现了Kannel，并做了一个demo。可惜公司时局变化，这一切都变得无足轻重了。

# awk&sed&grep

这三个工具是文本处理中用的比较多的工具，各有各的特色，且都支持正则表达式。

一般来说，行处理优先考虑使用sed和grep，列处理优先考虑使用awk。通常情况下，组合使用多个命令，其命令编写的难度小于只使用一个命令。比如sed和grep也可以进行列处理，但语法难度远超awk，反之亦然。

这里不打算列出各个命令的选项，而仅列出使用它们的一些示例：

这里假设我们有一文件名为ab。

## awk

{% highlight bash %}
awk '{print $1}' ab #显示第一列
{% endhighlight %}

## sed

{% highlight bash %}
sed '1d' ab #删除第一行 
sed '$d' ab #删除最后一行
sed '1,2d' ab #删除第一行到第二行
sed '2,$d' ab #删除第二行到最后一行

sed -n '1p' ab    #显示第一行 
sed -n '$p' ab    #显示最后一行
sed -n '1,2p' ab  #显示第一行到第二行
sed -n '2,$p' ab  #显示第二行到最后一行

sed -n '/ruby/p' ab #查询包括关键字ruby所在所有行
sed -n '/\$/p' ab #查询包括关键字$所在所有行，使用反斜线\屏蔽特殊含义

sed -n '/ruby/p' ab | sed 's/ruby/bird/g'    #替换ruby为bird
sed -n '/ruby/p' ab | sed 's/ruby//g'        #删除ruby

sed -e 's/.$//' mydos.txt > myunix.txt #dos->unix
{% endhighlight %}

## grep

{% highlight bash %}
grep 'ruby' ab #查询包括关键字ruby所在所有行
grep -nri 'ruby' #n 显示行号，r 子目录搜索，i 忽略大小写
{% endhighlight %}

## 综合

{% highlight bash %}
ip addr show br-lan | grep 'inet ' | awk  '{print $2}' | sed 's/\/.*//g'
{% endhighlight %}

# Win10历险记

我大概在2015年4、5月间，听说了Win10免费升级的消息。于是一直很期待7月29日的到来。果然到了29日当天下午的时候，公司电脑就收到了升级的通知。然而由于网速不给力，当天并未对公司电脑进行升级。倒是晚上在家里的电脑上，虽然耗时2小时，但却一路顺利的升级成功。

Win10给人的第一感觉，其实和Win8差不多，只不过加了个更像Win7的开始菜单而已。不过既来之则安之，一段时间用下来，总算还是要比Win7强不少的。

又过了几天，公司的电脑也升级成功。正得意间，忽然发现VirtualBox在Win10下工作不正常。查了VirtualBox官网方知，其目前尚不支持Win10 Host。于是不得不重新降级到Win7。看来尝鲜也是有得有失的。对于工作用的电脑，有的时候够用就好，没必要什么都求新的。


