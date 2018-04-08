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

Lazy Evaluation

next\(\)

```js
const makeNumbers = () => {
  let n = 0
  return {next: () => {
    n += 1
    return n
  }
}
numbers = makeNumbers()
numbers.next() // 1
numbers.next() // 2
numbers.next() // 3

// function generatiors
function* numbers() {
  let n = 0
  while(true) {
    n += 1
    yield n 
  }
}
```



