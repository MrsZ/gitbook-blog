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

