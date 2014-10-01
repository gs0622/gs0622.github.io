---
layout: post
title: "Intel I217-LM ethernet on Ubuntu 12.04"
date: 2014-09-09 19:04:52 +0800
comments: true
categories: Ubuntu Linux
---

If you're using Intel I217-LM ethernet on Ubuntu 12.04 LTS, you might get trouble says eth0 is not working on Linux kernel 3.2.x

<!--more-->

## Problem
I used 'lshw' and 'ifconfig' ensured it is detected on PCI but not in NetworkManager

    $ sudo lshw -C network
      *-network
       description: Ethernet interface
       product: Ethernet Connection I217-LM
       vendor: Intel Corporation
       physical id: 19
       bus info: pci@0000:00:19.0
       logical name: eth0
    ...
    $ ifconfig
    lo      Link encap:Local Loopback
            inet addr:127.0.0.1  Mask:255.0.0.0
            inet6 addr: ::1/128 Scope:Host
            UP LOOPBACK RUNNING  MTU:16436  Metric:1
            RX packets:223 errors:0 dropped:0 overruns:0 frame:0
            TX packets:223 errors:0 dropped:0 overruns:0 carrier:0
            collisions:0 txqueuelen:0
            RX bytes:141166 (141.1 KB)  TX bytes:141166 (141.1 KB)
    wlan0   Link encap:Ethernet  HWaddr xx:xx:xx:xx:xx:xx
            UP BROADCAST MULTICAST  MTU:1500  Metric:1
            RX packets:0 errors:0 dropped:0 overruns:0 frame:0
            TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
            collisions:0 txqueuelen:1000
            RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)

## Solution
By [StackOverflow](http://askubuntu.com/questions/310442/intel-i217lm-ethernet-controller-not-detected-by-ubuntu-12-04lts?#315922) I found potential cause due to I217 driver available since Linux 3.5.x however my Ubuntu 12.04 still using 3.2.0-29, probably it could be found in linux-backports-modules however I did not go the way.

I followed the hint to [Intel e1000e drivers page](http://www.intel.com/support/network/sb/cs-032514.htm), get the source then built on my laptop

    $ tar zxf e1000e-<x.x.x>.tar.gz
    $ cd e1000e-<x.x.x>/src/
    $ sudo make install
    $ modprobe e1000e
    $ ifconfig

Have fun on your eth0
