---
title: Enable coredump on ubuntu 16.04
author: will
date: 2017-07-15T02:35:52+00:00
url: /2017/07/15/enable-coredump-on-ubuntu-16.04/
categories:
  - tech
tags:
  - coredump
  - system
  - ubuntu

---
Coredump file is useful for debuging program crash. This post will show several settings related to coredump.

## Enable coredump

If you run program from shell , enable coredump via `unlimit  -c unlimited`， then check `unlimit -a | grep core`, if it shows `unlimited`, coredump is enabled for your current session.

If your program is hosted by systemd, you need to edit your program&#8217;s service unit file&#8217;s `[Service]` section, add `LimitCORE=infinity` to enable coredump.

## coredump location

Coredump file&#8217;s location is determined by kernerl parameter `kernel.core_pattern`.

On ubuntu 16.04 `kernel.core_pattern` default value is `|/usr/share/apport/apport %p %s %c %P`. Leading `|` means pass coredump file to following program. `%p %c %P` is used to create dump filename, their meaning can check via `man core`. apport will save dump file in /var/crash

If your default disk partition don&#8217;t have enough space to hold dump file, you can change `kernel.core_pattern` to another location, eg: `/mnt/core/%e-%t.%P`. If redis-server crashes, the dump file will be something like /mnt/core/redis-server-1500000000.1452. Also ensure crash process&#8217;s running user have write privilege on target location.

## systemd-coredump

You can install systemd-coredump to control dump file deeply, like: size, compression&#8230;.

Its config file is /etc/systemd/coredump.conf.

After install, it will change `kernel.core_pattern` to `|/lib/systemd/systemd-coredump %P %u %g %s %t 9223372036854775808 %e`.

By default it will save dump file in /var/lib/systemd/coredump/. But I didn&#8217;t find how to modify it to a customize location other than journal log.

After dumped, you can retrive dump file via `coredumpctl` command.

## Trigger process dump core manually.

Send siginal: `sudo kill -s SIGSEGV   {pid}`, it will crash process and save coredump.

Or `gcore {pid}`, it will make process save core file in current dir, won&#8217;t crash it.

## Attach coredump file to gdb

Very simple, if the process is redis, and its binary is `/usr/local/bin/redis-server`, dump file is `core`. Just `gdb /usr/local/bin/redis-server core`, needn&#8217;t config file. Then you can debug process memory when it crashed.
