```js
const head = ([x]) => x
const array = [1,2,3,4,5]
head(array) // 1
```

```js
const pipe = (fns) => (x) => fns.reduce((v, f) => f(v), x)
```

curry

```js
const add = R.curry((a, b) => a + b)
add(1, 2) // => 3
const add1 = add(1)
add1(2) // => 3
add1(10) // => 11
```



