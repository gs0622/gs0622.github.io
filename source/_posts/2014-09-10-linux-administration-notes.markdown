---
layout: post
title: "Linux administration notes"
date: 2014-09-10 11:28:23 +0800
comments: true
categories: Linux Ubuntu
---

Here is a memo of Linux workstation administration FAQs

<!--more-->

## Add new hard disk

#### Find new disk to setup
    $ sudo fdisk -l
{%img /images/20140910_list_partition.png 600 500 find new disk to setup %}

#### Create extend/logical partition
    Command: n -> e -> enter (default) -> enter (default)
{%img /images/20140910_ext_partition.png 600 500 create extended partition %}

    Command: n -> l -> enter (default) -> enter (default)
{%img /images/20140910_logical_partition.png 600 500 create logical partition %}

#### Exame then write partition table to disk
    Command: p (print) -> w (write)
{%img /images/20140910_write_table.png 600 500 exame then write partition table %}

#### Format new disk to ext4
    $ sudo mkfs.ext4 /dev/sdb5  # Notice! change sdb to sdX depend on your case
{%img /images/20140910_format_disk.png 600 500 exame partition table %}

#### Mount new disk
    $ mkdir -p /mydisk
    $ chmod 777 /mydisk
    $ mount -t ext4 /dev/sdb5 /mydisk

#### Add disk into fstab by UUID
    $ sudo blkid
    $ sudo vim /etc/fstab   # add 128-bit UUID of /dev/sdb5 into last line
    $ tail -n 1 /etc/fstab
    UUID=a1cf9f6e-dxxxx-xxxx-xxxx-xxxxxxx1eccf /mydisk  ext4    errors=remount-ro   0   1
{%img /images/20140910_find_uuid.png 600 500 find uuid %}

## Evaluate disk I/O performance
#### read benchmark
    $ sudo hdparm -Tt /dev/sdb
    /dev/sdb:
     Timing cached reads:   30414 MB in  1.99 seconds = 15289.37 MB/sec
     Timing buffered disk reads: 1046 MB in  3.00 seconds = 348.23 MB/sec
    $ sudo hdparm -Tt --direct /dev/sdb
    /dev/sdb:
     Timing O_DIRECT cached reads:   996 MB in  2.00 seconds = 497.87 MB/sec
     Timing O_DIRECT disk reads: 1444 MB in  3.00 seconds = 480.71 MB/sec
The **-T** is for **cached read test** while **-t** is for **buffered read**.
Second example with **--direct** which means assigned O_DIRECT flag in test

#### write benchmark
    $ dd if=/dev/zero of=/tmp/output conv=fdatasync bs=4k count=1M; rm -f /tmp/outut
    1048576+0 records in
    1048576+0 records out
    4294967296 bytes (4.3 GB) copied, 32.0625 s, 134 MB/s
    $ dd if=/dev/zero of=/ssd/output conv=fdatasync bs=4k count=1M; rm -f /ssd/output
    1048576+0 records in
    1048576+0 records out
    4294967296 bytes (4.3 GB) copied, 8.62645 s, 498 MB/s
First example I tested my system disk whick is 3.5" HDD, while second one I tested on SSD.
