# Find keys matching pattern

Redis commnad:`keys Pattern`, return all keys matching pattern.

Example code in Python, find keys matching `hello:*`:

```python
>>> import redis
>>> r = redis.StrictRedis()
>>> r.keys('hello:*')
```

*Warning*: use is in production carefully because it might affect performance.
