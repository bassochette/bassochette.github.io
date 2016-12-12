---
layout: post
title: "[cloud 66] cx toolbelt commands"
description: ""
category: "memo"
tags: ["cli", "cloud66", "cx toolbelt", "cx", "ops", "cheatsheet"]
---
{% include JB/setup %}

- List containers for a stack

```bash
$ cx containers list -s "stack name" -e staging|production
(staging|production)
SERVICE  SERVER  NAME                           CONTAINER ID      CONTAINER_NET_IP  DOCKER_IP   STARTED AT    HEALTH
web      Merlin  web.careful-tough-wildebeest   9b70386d62e26e7…  25.0.0.201        172.17.0.5  Dec 11 15:55  Unverified
web      Merlin  web.determined-romantic-heron  41cda7a47ae6041…  25.0.0.47         172.17.0.6  Dec 11 15:55  Unverified
```

- Get shell on target container

```bash
$ cx containers exec -s "Stack name" -e staging|production containerId9b70386d62e26e7 /bin/bash
Running exec on container...
(staging|production)
Note: you may need to push <enter> to view output after the connection completes..
root@9b70386d62e2:/usr/src/app#
```

- Redeploy

```bash
$ cx redeploy -s "Stack name" -e staging|production
(staging|production)
Stack starting redeployment
```

### Documentation:
- http://help.cloud66.com/category/toolbelt
