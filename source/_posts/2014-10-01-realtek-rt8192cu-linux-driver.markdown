---
layout: post
title: "Realtek rt8192cu Linux driver"
date: 2014-10-01 17:52:04 +0800
comments: true
categories: Ubuntu Linux
---

I got ASUS Wireless-N USB dongle couple months ago, thought it is supported in Linux, however I have no luck to enable it no matter on Ubuntu 12.04 nor 14.04 LTS.

<!--more-->

As the box cover claimed Linux supported, someday I put the dongle on my Ubuntu machines then found it has no reaction while plugged in.

{%img /images/20141001_asus_box.jpg 300 200 asus box %}
{%img /images/20141001_asus_dongle.jpg 300 200 asus dongle %}

I dug into both CD-ROM and Realtek website, well, driver source is quite old, even not able to build in new kernel (3.13+)

Occasionally I found there are lovely maintainers [Janez Troha](https://github.com/dz0ny) and [Stefan Keller](https://github.com/skeller), they did great jobs hosting a project maintaining rt8192cu driver, and further more applied [DKMS](http://en.wikipedia.org/wiki/Dynamic_Kernel_Module_Support) method.

Here is short note to enable the Wifi dongle by [Realtek driver for 8192cu / 8188cu devices](https://github.com/dz0ny/rt8192cu) 

#### Prerequisites
    $ sudo apt-get install git build-essential linux-headers-generic dkms
#### Get driver source
    $ git clone https://github.com/dz0ny/rt8192cu.git --depth 1
    $ cd rt8192cu
#### Easy install (DKMS)
    $ sudo make dkms
#### Hard install (traditional, non-DKMS)
    $ sudo make install

-enjoy

