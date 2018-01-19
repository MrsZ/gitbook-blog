Express

4xx error, respond reason to user directly

5xx error, respond error uuid to user and only show internal error, but log the error message to system

Define the error class

```js
const BadRequestError = function BadRequestError(message) {
  this.message = message || 'Bad request';
  this.name = 'BadRequestError';
  this.statusCode = 400;
  Error.captureStackTrace(this, BadRequestError);
};
BadRequestError.prototype = Object.create(Error.prototype);
BadRequestError.prototype.constructor = BadRequestError;

const UnauthorizedError = function UnauthorizedError(message) {
  this.message = message || 'Unauthorized';
  this.name = 'UnauthorizedError';
  this.statusCode = 401;
  Error.captureStackTrace(this, UnauthorizedError);
};
UnauthorizedError.prototype = Object.create(Error.prototype);
UnauthorizedError.prototype.constructor = UnauthorizedError;

const ForbiddenError = function ForbiddenError(message) {
  this.message = message || 'Forbidden';
  this.name = 'ForbiddenError';
  this.statusCode = 403;
  Error.captureStackTrace(this, ForbiddenError);
};
ForbiddenError.prototype = Object.create(Error.prototype);
ForbiddenError.prototype.constructor = ForbiddenError;

const NotFoundError = function NotFoundError(message) {
  this.message = message || 'Not found';
  this.name = 'NotFoundError';
  this.statusCode = 404;
  Error.captureStackTrace(this, NotFoundError);
};
NotFoundError.prototype = Object.create(Error.prototype);
NotFoundError.prototype.constructor = NotFoundError;

const ConflictError = function ConflictError(message) {
  this.message = message || 'Already exists';
  this.name = 'ConflictError';
  this.statusCode = 409;
  Error.captureStackTrace(this, ConflictError);
};
ConflictError.prototype = Object.create(Error.prototype);
ConflictError.prototype.constructor = ConflictError;

const InternalError = function InternalError(message) {
  this.message = message || 'Internal error';
  this.name = 'InternalError';
  this.statusCode = 500;
  Error.captureStackTrace(this, InternalError);
};
InternalError.prototype = Object.create(Error.prototype);
InternalError.prototype.constructor = InternalError;

module.exports = {
  BadRequestError,
  UnauthorizedError,
  ForbiddenError,
  NotFoundError,
  ConflictError,
  InternalError,
};

```

```js
new NotFoundError('api not found');
```

Promise

promise can use multiple catch in one chain

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

swagger error format

```
{
    "name": "JsonWebTokenError",
    "message": "jwt must be provided",
    "code": "server_error",
    "statusCode": 403
}
```



