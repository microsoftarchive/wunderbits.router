wunderbits.router
---

badges...

A simple and fast client side router that processes URL changes with a *middleware chain*.

## Getting started

First, install from npm.

```
$ npm install --save wunderbits.router
```

Create a *middleware function*.

```javascript
var myMiddleware = function (req, next) {

  console.log('the request url is ' + req.url);
  next();
};
```

Add and start the router.

```javascript
var Router = require('wunderbits.router').Router;
var MyRouter = Router.extend({
  'handlers': [
    myMiddleware
  ]
});

var router = new MyRouter();
router.start();
```

## Handle only specific urls

Execute a handler only when the url **exactly matches** a string.

```javascript
var MyRouter = Router.extend({
  'handlers': [
    {
      "handler": myMiddleware,
      "url": "/foo/bar"
    }
  ]
});
```

## Pattern matching and variables

Execute a handler only when the url **matches** a pattern, and extract params from the url string.

```javascript
function myMiddleware (req, next) {

  console.log(req.params.id);
  next();
}

var MyRouter = Router.extend({
  'handlers': [
    {
      "handler": myMiddleware,
      "pattern": /^\/foo\/:id/
    }
  ]
});
```

## Use handler constructors

If you want to fit your handlers into a class-based system, you can define a ```handlerConstructors``` object and reference it with ```handlerName#methodName```.

```javascript
var MyHandler = require('wunderbits.core').Klass.extend({
  'doSomething': function (req, next) {
    // your awesome logic goes in here...
    next();
  }
});

var MyRouter = Router.extend({
  "handleConstructors": {
    "foo": MyHandler
  },
  "handlers": [
    "foo#doSomething"
  ]
});
```

---

## Develop and contribute

1. First, fork this repo.
2. Implement something awesome
3. Write tests and run them with ```npm test```
4. Submit a pull request

### Credits

Author: [Adam Renklint](http://adamrenklint.com)

### License

Copyright (c) 2014 6 Wunderkinder GmbH

Permission is hereby granted, free of charge, to any person
obtaining a copy of this software and associated documentation
files (the "Software"), to deal in the Software without
restriction, including without limitation the rights to use,
copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the
Software is furnished to do so, subject to the following
conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES
OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT
HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY,
WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR
OTHER DEALINGS IN THE SOFTWARE.
