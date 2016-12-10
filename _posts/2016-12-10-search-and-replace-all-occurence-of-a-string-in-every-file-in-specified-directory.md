---
layout: post
title: "Search and replace all occurence of a string in every file in specified directory"
description: ""
category: "memo"
tags: ["osx", "cli"]
---
{% include JB/setup %}

```
$ grep -ilr "sourceString" * | xargs -I@ sed -i '' 's/sourceString/targetString/g' @
```
