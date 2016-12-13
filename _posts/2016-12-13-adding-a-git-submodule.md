---
layout: post
title: "Adding a git submodule"
description: ""
category:
tags: ["git", "git submodules", "cli", "dependencies", "dependency management", node]
---
{% include JB/setup %}


# sample project architecture

```
+ node_modules
+ lib

+ ux
  + subsite *submodule goes here*

server.js
```

# Adding the module

```bash
# Reference the submodule in git
$ git submodule add username@url:repo target/folder
# required?
$ git submodule init
# pull the code
$ git submodule update
```

## ❗💢 ⁉️ note for node repository ❗💢 ⁉️

don't forget to run npm install in submodule

```bash
$ cd path/to/submodule
$ npm install
```

# Cloning a repo with submodules:

```bash
$ git clone --recursive path/to/remote/repo [local/path]
```

# Documentation
- https://chrisjean.com/git-submodules-adding-using-removing-and-updating/ ⭐⭐⭐⭐⭐
- https://git-scm.com/docs/git-submodule
- https://github.com/npm/npm/issues/6700
