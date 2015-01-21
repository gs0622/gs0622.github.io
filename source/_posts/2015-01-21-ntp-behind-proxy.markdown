---
layout: post
title: "NTP behind proxy"
date: 2015-01-21 17:32:43 +0800
comments: true
categories: linux ubuntu ntpdate
---

Adventitiously I observed my desktop cannot do NTP update, suspecting
it is because of proxy. I did some triage then google.

Credit/refer to 
[How to use ntpdate behind a proxy?](http://superuser.com/questions/307158/how-to-use-ntpdate-behind-a-proxy)

<!--more-->

By triage, switch off NTP, modify time, then turn on NTP via system date/time setting is not working 
    $ dmesg | tail 
    [1328911.777687] systemd-timedated[8385]: Set NTP to disabled
    [1328918.627650] systemd-timedated[8385]: Changed local time to Wed Jan 21 17:26:35 2015
    [1328953.967353] systemd-timedated[8385]: Set NTP to enabled

Turns out there is wonderful conjuration using http header
    $ sudo date -s "$(curl -sD - google.com | grep ^Date: | cut -d' ' -f3-6)Z"
    Wed Jan 21 18:45:45 CST 2015

