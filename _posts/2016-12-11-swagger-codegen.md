---
layout: post
title: "Swagger codegen"
description: ""
category: "memo"
tags: ["swagger", "openAPI", "SDK", "swagger.io", "swagger-codegen", "swagger-ui", "php", "ruby", "js", "docker", "github"]
---
{% include JB/setup %}

## Tools
### swagger editor

- Live Demo: http://editor.swagger.io/

- Github repo: https://github.com/swagger-api/swagger-editor

- Docker hub:https://hub.docker.com/r/swaggerapi/swagger-editor/

### swagger ui

- Live demo: http://petstore.swagger.io/

- Github Repo: https://github.com/swagger-api/swagger-ui

- Docker hub: https://hub.docker.com/r/schickling/swagger-ui/

## Documentation

Swagger reference: http://swagger.io/specification/

## Generating SDKS

### Ruby
#### *OSX ONLY* using swagger-codegen brew package

- https://github.com/swagger-api/swagger-codegen#os-x-users

```
$ brew install swagger-codegen

$ swagger-codegen generate -i http://petstore.swagger.io/v2/swagger.json -l ruby -o /tmp/test/
```


### PHP
#### Using the swagger editor

- http://swagger-editor-d6c6fb96-1.c4b33edc.cont.dockerapp.io:32769/#/

![Swagger editor home screen]({{ site.url }}/assets/swagger-editor/uber.png)

![Swagger editor generate php client]({{ site.url }}/assets/swagger-editor/generate-php.png)

![Swagger editor generate php client download]({{ site.url }}/assets/swagger-editor/generate-php-downloads.png)


### Javascript
#### using swagger-js npm module:
- https://github.com/swagger-api/swagger-js

```shell
$ npm install --save swagger-client
```

```Javascript
"use strict"
const Swagger = require('swagger-client');

new Swagger({
    usePromise: true,
    url: SWAGGER_JSON_URL
  })
  .then(
    client => {
      client.tag.operationId(params)
        .then(
          response => {
            /*
              DO something...
            */
          }
        )
    }
  )
  .catch(
    error => {
      /*
      Handle errors
      */
    }
  );
```

## references
- https://github.com/swagger-api/swagger-codegen
- https://github.com/swagger-api/swagger-js
- https://github.com/wcandillon/swagger-js-codegen
