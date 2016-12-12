---
layout: post
title: "[OSX] find and kill process running on port osx"
description: " "
category: "memo"
tags: ["osx", "cli"]
---
{% include JB/setup %}

### Find pid of process running on port:

example port 3000

```
$ lsof -i :3000
COMMAND   PID   USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
node    *81602* julien   14u  IPv6 0x669792e160564ee3      0t0  TCP *:hbci (LISTEN)
```

### Kill the process on found pid

```
$ kill -9 81602
$ echo $?
0
```
