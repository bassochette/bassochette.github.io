---
layout: post
title: "the node path trick"
description: "Use NODE_PATH variable to ease dependencies in node js"
category: node
tags: ["nodejs", "typescript", "trick"]
---
{% include JB/setup %}

* Let say you have a file structure like this one:

```
index.ts
libs/
    services/
        superService.ts
    utils/
        parser.ts
```

* you go `NODE_PATH=libs ts-node index` (not a ts thing but we both use ts)

All import are now relative to the path specified in the NODE_PATH variable.

and then instead of importing like this:

``` libs/services/superService.ts
import phone from "../utils/parser";

// more code
```

* yu can import like that:

```libs/services/superService.ts
import phone from "utils/parser";

//more code
```

``` index.ts
import doStuff from "services/superService";
import phone from "utils/parser";

// more code
```
