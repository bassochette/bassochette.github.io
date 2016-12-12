---
layout: post
category : memo
tagline: "Unit testing express ASYNC middleware function with mocha, chai and sinon"
tags : [node, unit-test, js, chai, mocha, sinon, express, middleware, babel, async]
---
{% include JB/setup %}

# Description

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

# code

## *middleware/setSession.js*

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
  return validationService.execute(token)
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

# test

## *spec/middleware/setSessionSpec.js*

```javascript
"use strict";
// sinon mocha and chai are configured in the helper module
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
        let request = {
          headers: {
            token: "invalid token"
          }
        };
        let response = {
          status: (code) => {
            return {
              json: (data) => {
                return data
              }
            }
          }
        }

        let statusSpy = sinon.spy(response, "status");
        setSessionMiddleware(
          request,
          response,
          () => {
            // will never execute
          }
        )
        .then(
          resp => {
            statusSpy.restore()
  					    sinon.assert.calledOnce(statusSpy);
  					    done();
          }
        )
      }
    )
  }
)
```

## Run the test

```bash
$ NODE_ENV=test mocha --require babel-core/register spec/middleware/setSessionSpec.js
```


# Documentation:
- https://semaphoreci.com/community/tutorials/best-practices-for-spies-stubs-and-mocks-in-sinon-js
- jsdoc promise : https://github.com/jsdoc3/jsdoc/issues/509
- sinon: http://sinonjs.org/docs/
