---
layout: post
title: "Linux administration notes"
date: 2014-09-10 11:28:23 +0800
comments: true
categories: 
---

Here is a memo of Linux workstation administration FAQs

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

