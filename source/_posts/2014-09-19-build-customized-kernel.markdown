---
layout: post
title: "Build customized kernel"
date: 2014-09-19 09:28:33 +0800
comments: true
categories: Ubuntu Linux
---

A quick note to build your customized Linux kernel on Ubuntu system.
Below are refer to [GitKernelBuild](https://wiki.ubuntu.com/KernelTeam/GitKernelBuild)

<!--more-->

## Build kernel
#### Checkout upstream kernel
    $ git clone git://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git
    $ cd linux
    $ git checkout TAG/COMMIT  # up on your case, ex: git checkout v3.17-rc5
#### Copy default config
    $ cp /boot/config-`uname -r` .config
    $ make oldconfig
    $ # (optional) change your kernel flavor continue by 'make menuconfig'
    $ #            in my case I skip that simply want to build latest kernel
#### Make kernel packages
    $ make -j `getconf _NPROCESSORS_ONLN` deb-pkg LOCALVERSION=-harry

now wait and grab a coffee, it takes time
after then you will see couple *.deb* file in upper folder

    $ ls -lh ../*.deb | awk '{print $5, "\t", $9}'
    944K   ../linux-firmware-image-3.17.0-rc5-harry_3.17.0-rc5-harry-3_amd64.deb
    6.4M   ../linux-headers-3.17.0-rc5-harry_3.17.0-rc5-harry-3_amd64.deb
    353M   ../linux-image-3.17.0-rc5-harry_3.17.0-rc5-harry-3_amd64.deb
    35M    ../linux-image-3.17.0-rc5-harry-dbg_3.17.0-rc5-harry-3_amd64.deb
    750K   ../linux-libc-dev_3.17.0-rc5-harry-3_amd64.deb

#### Install kernel packages
    $ sudo dpkg -i ../linux-image-3.17.0-rc5-harry_3.17.0-rc5-harry-3_amd64.deb
    $ sudo dpkg -i ../linux-headers-3.17.0-rc5-harry_3.17.0-rc5-harry-3_amd64.deb

once done, reboot then cross fingers

    $ sudo reboot

#### Remove kernel packages
You might want to remove customized kernel

    $ dpkg -l | grep harry
    ii  linux-headers-3.17.0-rc5-harry                        3.17.0-rc5-harry-3                                  amd64        Linux kernel headers for 3.17.0-rc5-harry on amd64
    ii  linux-image-3.17.0-rc5-harry                          3.17.0-rc5-harry-3                                  amd64        Linux kernel, version 3.17.0-rc5-harry
    $ sudo dpkg --purge linux-headers-3.17.0-rc5-harry
    $ sudo dpkg --purge linux-image-3.17.0-rc5-harry

