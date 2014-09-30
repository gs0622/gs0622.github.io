---
layout: post
title: "Chromium OS build notes"
date: 2014-08-27 20:01:09 +0800
comments: true
categories: Chromium_OS Linux
---

Basically this is short notes about building Chromium OS (a.k.a Chrome OS), all refer to [Chromium OS Developer Guide](http://www.chromium.org/chromium-os/developer-guide)

<!--more-->

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
    $ export BOARD=x86-generic      # change board depend on your device, pick one from overlays
    $ ./setup_board --board=${BOARD}
    $ ./build_packages --board=${BOARD}
    $ ./build_image --board=${BOARD} --noenable_rootfs_verification dev
#### download
    $ cros flash usb:// ${BOARD}/latest     # then boot your device by this USB key
## Clean
    $ # delete chroot, do *NOT* use rm -rf chroot
    $ cros_sdk --delete

## Enlarge ccache size
ccache is used to speedup chromiumos 2nd build, typical build will spend 9GB space, however the default size is 1GB only, you can enlarge it manually

    $ ccache --max-size=10G
    $ export CCACHE_DIR=/var/cache/distfiles/ccache
    $ ccache -s

