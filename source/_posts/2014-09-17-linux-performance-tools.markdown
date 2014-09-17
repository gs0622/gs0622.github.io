---
layout: post
title: "Linux Performance Tools"
date: 2014-09-17 18:27:04 +0800
comments: true
categories: Linux Performance
---

[Brendan Gregg](http://www.brendangregg.com/) 於今年八月在[LinuxCon](http://events.linuxfoundation.org/events/linuxcon-north-america)所給的演說，內容涵蓋high-level overview到常用基本指令可讓工程師知道如何分析系統效能瓶頸。

<iframe src="//www.slideshare.net/slideshow/embed_code/38175637" width="427" height="356" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="https://www.slideshare.net/brendangregg/linux-performance-tools" title="Linux Performance Tools" target="_blank">Linux Performance Tools</a> </strong> from <strong><a href="http://www.slideshare.net/brendangregg" target="_blank">brendangregg</a></strong> </div>

<!--more-->

讀者可從基本的uptime, top, ps, vmstat, mpstat, free，到進階練習strace/ltrace, tcpdump, netstat, nicstat, pidstat, iotop, slabtop ...etc.

尤其開頭第二頁的big picture做得相當棒，可以當成cheat sheet
{%img http http://www.brendangregg.com/Perf/linux_observability_tools.png 600 500 linux_observability_tools %}

**SIDE NOTE**: 緣起於我想了解目前的build machine是CPU bound, memory bound, I/O bound, 我用了vmstat, top, free, tmux不斷的實驗與觀察，輾轉又發現這篇投影片。
