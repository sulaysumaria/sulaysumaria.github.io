---
layout: post
title: "Find Public IP-Address From CLI"
categories: [CLI]
permalink: /find-public-ip-address-from-cli
---

There are many ways to find out your public IP address or wan (Wide Area Network) IP on a Linux or Unix-like operating systems such as FreeBSD, OpenBSD, NetBSD, Apple OS X, and others.

Use below command:

```bash
$ dig +short myip.opendns.com @resolver1.opendns.com
# or
$ dig TXT +short o-o.myaddr.l.google.com @ns1.google.com
```

This comamnds work on any UNIX-like operating system.
