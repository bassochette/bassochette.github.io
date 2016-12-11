---
layout: post
category : ❓ wtf 🍀
tagline: "Unit testing express middleware function with mocha, chai"
tags : [node, unit-test, js, chai, mocha, sinon, express, middleware]
---
{% include JB/setup %}

### Description

This function fetch a sessionToken sent via header.
If none are provided the request is go threw without a session.
If the token is valid a session is set to the request.
If the token is invalid, a 403 http code is sent with a message.

The `execute` function implementation from the validate token service follow this interface:

```javascript
/**
 * @param {String} token
 * @return {Promise.<Object, Error>} - ES6 promise
 */
```

I try to only test the middleware function outside of express.
I am not trying to use a http request or load express but just test the behavior
of this function.

### code

#### middleware/setSession.js

```javascript
"use strict";
import validationService from "../services/validateToken";
import KEY_HEADER from "../constants/security";

export default function(request, response, next){
  let token = request.headers[KEY_HEADER] || false;
  if(!token) {
    request.session = false;
    return next()
  };
  validationService.execute(token)
    .then(
      session => {
        request.session = session;
        next()
      }
    )
    .catch(
      error => {
        response.status(403).json(
          {
            "message": "unauthorized"
          }
        )
      }
    )
}
```

### test

#### spec/middleware/setSessionSpec.js

```javascript
"use strict";
import helper from "../../helper";
import setSessionMiddleware from "../../../middleware/setSession"
describe(
  "Set Session middleware", (done) => {
    it(
      "set an empty session if no headers",
      () => {
        let request = {
          headers: {}
        };
        let response = {}
        setSessionMiddleware(
          request,
          response,
          () => {
            request.session.should.be.false;
            done();
          }
        )
      }
    );
    it(
      "set the session if the token is valid",
      () => {
        let request = {
          headers: {
            token: "validToken"
          }
        };
        let response = {};
        setSessionMiddleware(
          request,
          response,
          () => {
            request.session.should.be.an("object");
            done();
          }
        )
      }
    );
    it(
      "send 403 and message if the token is invalid",
      () => {
        setSessionMiddleware(
          request,
          response,
          () => {
            /*
              ISSUE:
              How to test the status is 403 a
              How to test the json function will be called with the message?
            */
          }
        )
      }
    )
  }
)
```

### Issue

- How can I test the response 403

### Solution

- none yet
- sinon? stub? spy?

#### Documentation:

- jsdoc promise : https://github.com/jsdoc3/jsdoc/issues/509
