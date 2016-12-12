---
layout: post
title: "[OSX] find and kill process running on port osx"
description: " "
category: "memo"
tags: ["osx", "cli", "lsof", "kill"]
---
{% include JB/setup %}

# Commands
## Find pid of process running on port:

example port 3000

```
$ lsof -i :3000
COMMAND   PID   USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
node    *81602* julien   14u  IPv6 0x669792e160564ee3      0t0  TCP *:hbci (LISTEN)
```

### lsof - *list open file*

from OSX man page

    * `-i :3000`: match internet address with port 3000

## Kill the process on found pid

```
$ kill -9 81602
$ echo $?
0
```

### kill - *terminate or signal a process*

from OSX man page

  * `-9 81609`: send KILL (-9) signal to process with PID 81609
