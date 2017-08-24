---
layout: post
title: "What's going on in my commit?"
author: "Julien"
date: 2017-08-24 11:34:06
tags:
- git
- tricks
---

You want to check what's in that specific commit without going on github, bitbucket, whatever...
here is the command my friend:

```bash
$ git show [options] <commit-id>
```

```
commit 52d9f0dca5d4aec38c1d5c550271f54a8017b372
Author: Julien Prugne <julien.prugne@gmail.com>
Date:   Tue Jun 27 11:52:07 2017 -0400

    quick update

    diff --git a/_posts/2017-06-27-the-node-path-trick.md b/_posts/2017-06-27-the-node-path-trick.md
    index 38d2f89..b71013e 100644
    --- a/_posts/2017-06-27-the-node-path-trick.md
    +++ b/_posts/2017-06-27-the-node-path-trick.md
    @@ -7,7 +7,7 @@ tags: ["nodejs", "typescript", "trick"]
     ---
      {% include JB/setup %}

      -Let say you have a file structure like this one:
      +* Let say you have a file structure like this one:

       ```
        index.ts
        @@ -18,17 +18,19 @@ libs/
                 parser.ts
                  ```

                  -you go `NODE_PATH=libs ts-node index` (not a ts thing but we both use ts)
                  +* you go `NODE_PATH=libs ts-node index` (not a ts thing but we both use ts)
                  +
                  +All import are now relative to the path specified in the NODE_PATH variable.


... 
```

source: https://git-scm.com/docs/git-show
