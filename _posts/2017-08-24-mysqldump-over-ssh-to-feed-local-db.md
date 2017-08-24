---
layout: post
title: "mysqldump over ssh to feed local db"
category: "memo"
date: 2017-08-24 14:12:05
tags:
- mysql 
- mysqldump 
- ssh 
- tips and tricks
---

```bash
ssh <username>@<host> mysqldump -u<db user> -p<db password> <db name> | mysql -u<db user> -p<db password> <db name>
```
