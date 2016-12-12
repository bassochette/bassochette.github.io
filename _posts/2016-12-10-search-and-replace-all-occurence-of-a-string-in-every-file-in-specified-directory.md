---
layout: post
title: "[OSX] Search and replace all occurence of a string in every file in specified directory"
description: ""
category: "memo"
tags: ["osx", "cli", "grep", "xargs", "sed"]
---
{% include JB/setup %}

# Command

```
$ grep -ilr "sourceString" * | xargs -I@ sed -i '' 's/sourceString/targetString/g' @
```

# description

## grep -- *file pattern searcher*

from OSX grep man page

  * `-i`: `--ignore-case` Perform case insensitive matching
  * `-l`: `--files-with-matches` Only the names of files containing selected lines are written to standard output.
  * `-r`: `-R`, `--recursive` Recursively search subdirectories.

## xargs -- *construct arguments list(s) and execute utility*

from OSX zargs man page

  * `-I@ ** @`:

## sed -- *stream editor*

from OSX man page

  * `-i ''`: specify backup extension. 0 length backup extension meaning no backup
  * `'s/sourceString/targetString/g'` : search and replace globally all occurences of `sourceString` by `targetString`
