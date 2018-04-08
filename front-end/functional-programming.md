```js
const head = ([x]) => x
const array = [1,2,3,4,5]
head(array) // 1
```

```js
const pipe = (fns) => (x) => fns.reduce((v, f) => f(v), x)
```



