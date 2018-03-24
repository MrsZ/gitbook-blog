Promise.all problem

```js
function promiseA() {
  return Promise.all([])
}

function () {
  return promiseA
  .then(([]) => {}) // 会在这里报错define
}

```



