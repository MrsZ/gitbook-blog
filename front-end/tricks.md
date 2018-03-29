promise easy load

```js

```

---

redis hmset pass params

```js
hmset(roomId, options, initValue = 0) {
      const k = key.vote.options(roomId);
      const optionArr = _.keys(options);
      const params = [];
      optionArr.forEach((option) => {
        params.push(option);
        params.push(initValue);
      });

      // optionA, 0, optionB, 0
      return redisClient.hmset(k, ...params);
    }
```



