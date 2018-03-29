promise easy load

```js
get(key, dbPromise, ...params) {
    return new Promise((resolve, reject) => {
      const redisTTL = 2400; // sec
      const ramTTL = 1000; // microsec
      const memoryResult = memoryCache.get(key);
      if (memoryResult) {
        if (!isJSON(memoryResult)) {
          return resolve(memoryResult);
        }
        return resolve(JSON.parse(memoryResult));
      }

      return redisClient.get(key)
        .then((cachedResult) => {
          if (cachedResult) {
            memoryCache.put(key, cachedResult, ramTTL);
            if (!isJSON(cachedResult)) {
              return resolve(cachedResult);
            }
            return resolve(JSON.parse(cachedResult));
          }

          return dbPromise(...params)
            .then((dbResult) => {
              redisClient.set(key, JSON.stringify(dbResult), 'EX', redisTTL);
              memoryCache.put(key, JSON.stringify(dbResult), ramTTL);
              return resolve(dbResult);
            })
            .catch(err => reject(err));
        })
        .catch(err => reject(err));
    });
  },
  del(key, dbPromise, ...params) {
    return Promise.all([
      redisClient.del(key),
      dbPromise(...params),
    ])
      .then(([success, instance]) =>
        Promise.resolve(instance))
      .catch(err => Promise.reject(err));
  },
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



