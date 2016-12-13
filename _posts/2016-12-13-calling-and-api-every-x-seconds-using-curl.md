---
layout: post
title: "[Curl] Calling an http api every X seconds using curl"
description: ""
category: memo
tags: ["cli", "bash", "inline scripting", "json", "http", "api", "curl", "python"]
---
{% include JB/setup %}

# Command

```bash
while true; do curl -X GET \
  -H "Content-Type: application/json" \
  -H "authorizationHader: $TOKEN" \
  $ENDPOINT_URL | python -m json.tool && sleep 60; done
```

# Explication

## Variables:

  * `ENDPOINT_URL`  https://api.ecma.com/v1/endpoint
  * `TOKEN`  s0meAuthenticationTokenJustHereToSetAnExampleHeader

## infinite loop

```bash
while true;
do
  # do stuff.
done
```

## Curl

  * `-X <command>`, `--request <command>` http verb. GET, POST, PUT, PATCH, DELETE, ...
  * `-H <header>`, `--header <header>`: set custom header

## python

  * `-m module-name` Searches sys.path for the named module and runs the corresponding .py file as a script
  * `json.tool` validate and pretty print python

## delay

  * `sleep _seconds_` suspend execution for _seconds_

# Documentation
- https://docs.python.org/2/library/json.html
- OSX python 2.7.12 man page
- OSX curl 7.43.0 man page
- OSX builtin man page
