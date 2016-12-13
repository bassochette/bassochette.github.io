---
layout: post
title: "[express] cors support with helmet"
description: ""
category: memo
tags: ["node", "javascript", "cors", "express", "express4.X", "helmet", "frameguard"]
---
{% include JB/setup %}


# error
```
Refused to display 'http://local.dev:8000' in a frame because it set 'X-Frame-Options' to 'SAMEORIGIN'.
```

# solution
```javascript
import express from "express";
import helmet from "helmet";

let app = express();
// ...
// other configs
// deny all framing
app.use(
  helmet(
    {
      frameguard: "deny"
    }
  )
)

// only allow SAMEORIGIN
app.use(
  helmet(
    {
      frameguard: "sameorigin"
    }
  )
)

// allow from one domain
app.use(
  helmet(
    {
      action: "allow-from",
      domain: "http://example.com"
    }
  )
)

// allow all origins // not working
app.use(helmet({
  frameguard: {
    action: "allow-from",
    domain: "*"
  }
}))

// other configs
// ...
```


# documentation
- https://helmetjs.github.io/docs/frameguard/
- https://github.com/helmetjs/helmet
- http://expressjs.com/
