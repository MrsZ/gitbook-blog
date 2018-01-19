Calculate running time

create a middleware

```js
var uuid = require('uuid'),
    common = require('../../lib/common');

/**
 * @TODO:
 * - move middleware to ignition?
 */
module.exports = function logRequest(req, res, next) {
    var startTime = Date.now(),
        requestId = req.get('X-Request-ID') || uuid.v1();

    function logResponse() {
        res.responseTime = (Date.now() - startTime) + 'ms';
        req.requestId = requestId;
        req.userId = req.user ? (req.user.id ? req.user.id : req.user) : null;

        if (req.err && req.err.statusCode !== 404) {
            common.logging.error({req: req, res: res, err: req.err});
        } else {
            common.logging.info({req: req, res: res});
        }

        res.removeListener('finish', logResponse);
        res.removeListener('close', logResponse);
    }

    res.on('finish', logResponse);
    res.on('close', logResponse);
    next();
};
```

Error Handling

use middleware

use next\(\) to pass error to error handler. If want to end the process, need return next\(\).

Error-handling middleware always takes four arguments. You must provide four arguments to identify it as an error-handling middleware function. Even if you don’t need to use the next object, you must specify it to maintain the signature.

```js
const app = require('express')();

app.get('*', function(req, res, next) {
  // Reporting async errors *must* go through `next()`
  setImmediate(() => { next(new Error('woops')); });
});

app.use(function(error, req, res, next) {
  // Will get here
  res.json({ message: error.message });
});

app.listen(3000);
```



# Application

[Keystone](http://keystonejs.com/zh/) 

[Ghost](https://github.com/TryGhost/Ghost) 



