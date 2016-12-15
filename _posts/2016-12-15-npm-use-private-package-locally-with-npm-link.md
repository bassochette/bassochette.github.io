---
layout: post
title: "[NPM] use private package locally with npm link"
description: ""
category: memo
tags: [npm, NodeJs, javascript]
---
{% include JB/setup %}

# In the private module folder:

```
$ npm link
```
# Where the private module need to be used

```
$ npm link @user/package
$ npm rebuild
```
