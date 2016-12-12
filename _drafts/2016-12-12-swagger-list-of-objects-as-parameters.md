---
layout: post
title: "[Swagger] list of objects as parameters"
description: ""
category: "undefined"
tags: ["swagger", "yaml", "swagger-jsdoc"]
---
{% include JB/setup %}
# Problem:

### swagger.yaml
```yaml
#...
definitions:
  BatchUpdate:
    properties:
      payments:
        type: array
        items:
          $ref: "#/definitions/PaymentListPatch"
  PaymentListPatch:
    properties:
      amount:
        type: number
      recipientId:
        type: string
#...
```

```
Details
 Object
code:  "ANY_OF_MISSING"
 params: Array [0]
message:  "Not a valid schema items definition"
 path: Array [5]
0:  "definitions"
1:  "BatchUpdate"
2:  "properties"
3:  "payments"
4:  "items"
schemaId:  "http://swagger.io/v2/schema.json#"
 inner: Array [2]
 0: Object
code:  "OBJECT_ADDITIONAL_PROPERTIES"
 params: Array [1]
 0: Array [1]
message:  "Additional properties not allowed: schema"
 path: Array [7]
0:  "definitions"
1:  "BatchUpdate"
2:  "properties"
3:  "payments"
4:  "items"
5:  "properties"
6:  "recipient"
description:  "A deterministic version of a JSON Schema object."
 1: Object
code:  "INVALID_TYPE"
 params: Array [2]
0:  "array"
1:  "object"
message:  "Expected type array but found type object"
 path: Array [5]
0:  "definitions"
1:  "BatchUpdate"
2:  "properties"
3:  "payments"
4:  "items"
level: 900
type:  "Swagger Error"
description:  "Not a valid schema items definition"
lineNumber: 1202
```

# Solution:


# Documentation
## 👍 Relevant 👍

## 💢 Irrelevant 💢

## ❓ undef ❓
- http://stackoverflow.com/questions/38088771/swagger-yaml-schema-definition-for-object-without-a-fixed-property-list
- https://apihandyman.io/writing-openapi-swagger-specification-tutorial-part-4-advanced-data-modeling/
- http://stackoverflow.com/questions/27790643/define-a-property-with-a-mixed-data-type-in-swagger
- http://stackoverflow.com/questions/32502026/create-complex-types-definitions-in-swagger
- https://github.com/swagger-api/swagger-node/issues/370
- https://github.com/apigee-127/swagger-converter/issues/16
- https://github.com/geraintluff/tv4/issues/228
- https://github.com/swagger-api/swagger-ui/issues/294
