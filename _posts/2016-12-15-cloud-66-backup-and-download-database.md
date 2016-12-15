---
layout: post
title: "[Cloud 66] backup and download postgresql database"
description: ""
category: memo
tags: [cloud66, "cx toolbelt", database, backup, cli, postgresql, osx]
---
{% include JB/setup %}

# Create backup

```bash
$ cx backup new -s "Stack Name" -e environment
(staging)
queued for creation
```

# now we wait for the backup to be ready

```bash
$ cx backup list -s "Stack Name" -e environment
(staging)
*8311576*  postgresql  api_staging                Ok  Dec 15 11:20  Not Restored  Not Verified
8311575  redis                                  Ok  Dec 15 11:18  Not Restored  Not Verified
```

# Download the backup

```bash
$ cx backup download -s "Stack Name" -e staging *8311576* .
(staging)
Downloading TJJqXRigWV.tar to /Users/bassochette/cx_backups/tmp/8311576
Concatenating files to /Users/bassochette/cx_backups/backup_8311576.tar
Deleting /Users/bassochette/cx_backups/tmp/8311576
Done
```

# Decompress

```bash
$ cd ~/cx_backups
$ tar -xvvf backup_8311576.tar
x TEJqXRigWV/
x TEJqXRigWV/databases/
x TEJqXRigWV/databases/PostgreSQL/
x TEJqXRigWV/databases/PostgreSQL/api_staging.sql.gz

$ cd TJJqXRigWV/database/PostgreSQL
$ gunzip api_staging.sql.gz
```

# Restore locally

```bash
$ psql dbname < api_staging.sql
# lot's of logs
```

# Documentation

- http://help.cloud66.com/toolbelt/toolbelt-download-command
- OSX tar man page
- OSX gunzip man page
- https://www.postgresql.org/docs/8.1/static/backup.html
