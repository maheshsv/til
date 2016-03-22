# Transaction in Redis

Redis' [MULTI](http://redis.io/commands/MULTI) command is like tranasaction in some other relational database.

In `redis-cli`:

```bash
127.0.0.1:6379> multi
OK
127.0.0.1:6379> set k v
QUEUED
127.0.0.1:6379> incr k_counter
QUEUED
127.0.0.1:6379> exec
1) OK
2) (integer) 1
```

In Python, with [redis-py](https://github.com/andymccurdy/redis-py):

```python
>>> import redis
>>> pipe = r.pipeline()
>>> pipe.set('foo', 'bar')
>>> pipe.incr('counter')
>>> pipe.execute()
```
