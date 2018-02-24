use as cache

cache should set expire time



delete keys by pattern

```bash
redis-cli --raw keys 'PATTERN' | xargs redis-cli del 
```



