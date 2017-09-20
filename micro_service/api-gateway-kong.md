# API Gateway: Kong

[Kong](https://github.com/Mashape/kong) is scalable, open source micro-service API gateway. Essentially it's an [OpenResty](https://github.com/Mashape/kong) application, and OpenResty itself is a massively scalable web platform by extending Nginx with Lua.

Kong has very good [documentation](https://getkong.org/docs/). So I will not repeat them here. Below are some of the tricks I learned in the past few days playing with Kong.

```bash
# add an example API with http(httpie)
> http POST localhost:8001/apis name=example-api strip_uri=false upstream_url='http://httpbin.org' uris='/ip,/user-agent'
{
    "created_at": 1505889216556,
    "http_if_terminated": true,
    "https_only": false,
    "id": "b49b9591-b4a8-48b4-a477-15b534b5b40b",
    "name": "example-api",
    "preserve_host": false,
    "retries": 5,
    "strip_uri": false,
    "upstream_connect_timeout": 60000,
    "upstream_read_timeout": 60000,
    "upstream_send_timeout": 60000,
    "upstream_url": "http://httpbin.org",
    "uris": [
        "/ip",
        "/user-agent"
    ]
}

# test example-api through API Gateway proxy
> http localhost:8000/user-agent
HTTP/1.1 200 OK
Access-Control-Allow-Credentials: true
Access-Control-Allow-Origin: *
Connection: keep-alive
Content-Length: 35
Content-Type: application/json
Date: Wed, 20 Sep 2017 06:35:41 GMT
Server: meinheld/0.6.1
Via: kong/0.10.3
X-Kong-Proxy-Latency: 32
X-Kong-Upstream-Latency: 180
X-Powered-By: Flask
X-Processed-Time: 0.000519990921021

{
    "user-agent": "HTTPie/0.9.9"
}

```

### Lesson Learned

To support transparent proxy without specify target `Host` in request header, set `strip_uri` to `false` and don't specify `hosts` when creating APIs.

