Express

4xx error, respond reason to user directly

5xx error, respond error uuid to user and only show internal error, but log the error message to system

Define the error class

```js
const NotFoundError = function NotFoundError(message) {
    this.message = message || 'Not found';
    this.name = 'NotFoundError';
    Error.captureStackTrace(this, NotFoundError);
};
NotFoundError.prototype = Object.create(Error.prototype);
NotFoundError.prototype.constructor = NotFoundError;
```

Promise



# Process Unhandled Error

```js
process.on('unhandledRejection', (reason, p) => {
  // I just caught an unhandled promise rejection, since we already have fallback handler for unhandled errors (see below), let throw and let him handle that
  throw reason;
});
process.on('uncaughtException', (error) => {
  // I just received an error that was never handled, time to handle it and then decide whether a restart is needed
  errorManagement.handler.handleError(error);
  if (!errorManagement.handler.isTrustedError(error))
    process.exit(1);
});
```



