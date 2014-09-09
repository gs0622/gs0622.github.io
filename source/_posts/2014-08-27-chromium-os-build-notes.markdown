---
layout: post
title: "Chromium OS build notes"
date: 2014-08-27 20:01:09 +0800
comments: true
categories: 
---

Basically this is short notes about building Chromium OS (a.k.a Chrome OS), all refer to [Chromium OS Developer Guide](http://www.chromium.org/chromium-os/developer-guide)

## Environment
    $ sudo apt-get install git-core gitk git-gui subversion curl
    $ git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git
    $ export PATH=`pwd`/depot_tools:"$PATH"   # better to add it into .bashrc
## Source 
    $ mkdir -p chromiumos && cd chromiumos
    $ repo init -u https://chromium.googlesource.com/chromiumos/manifest.git --repo-url https://chromium.googlesource.com/external/repo.git
    $ repo sync
## Build
#### enter chroot
    $ ./chromite/bin/cros_sdk
#### board select
    $ export BOARD=x86-generic
    $ ./setup_board --board=${BOARD}
    $ ./build_packages --board=${BOARD}
    $ ./build_image --board=${BOARD} --noenable_rootfs_verification dev
#### download
    $ cros flash usb:// ${BOARD}/latest     # then boot your device by this USB key
## Clean
    $ # delete chroot, do *NOT* use rm -rf chroot
    $ cros_sdk --delete

TBD
