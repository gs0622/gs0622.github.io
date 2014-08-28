---
layout: post
title: "Chromium OS build notes"
date: 2014-08-27 20:01:09 +0800
comments: true
categories: 
---

Basically this is short notes about building Chromium OS (a.k.a Chrome OS), all refer to [Chromium OS Developer Guide](http://www.chromium.org/chromium-os/developer-guide)

## Source 
TBD
## Build
### enter chroot
    $ ./chromite/bin/cros_sdk
### board select
    $ export BOARD=x86-generic
    $ ./setup_board --board=${BOARD}
    $ ./build_packages --board=${BOARD}
    $ ./build_image --board=${BOARD} --noenable_rootfs_verification dev
</code>
## Download
TBD
