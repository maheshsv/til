# HTTP Post with Requests

[Requests](http://docs.python-requests.org/en/master/): HTTP for Humans. To do an HTTP Post with Requests:

```
import requests
requests.post('http://httpbin.org/post', data='abc')
```

Note that requests url need the protocal scheme `http://` part.
