# HTTP Tools

- [http://httpbin.org/](http://httpbin.org/) is a freely hosted HTTP Client Testing Service.
- [HTTPie](https://httpie.org/) is a command line HTTP Client.
- [POSTMAN](https://www.getpostman.com/) is yet another great tool for testing and developing HTTP APIs.

### `http` Synopsis:

```
$ http [flags] [METHOD] URL [ITEM [ITEM]]
```

HTTPie doc is [here](https://httpie.org/doc).

Examples:

### Get client IP from httpbin:

```bash
> http httpbin.org/ip

HTTP/1.1 200 OK
Access-Control-Allow-Credentials: true
Access-Control-Allow-Origin: *
Connection: keep-alive
Content-Length: 32
Content-Type: application/json
Date: Tue, 19 Sep 2017 03:36:53 GMT
Server: meinheld/0.6.1
Via: 1.1 vegur
X-Powered-By: Flask
X-Processed-Time: 0.000452995300293

{
    "origin": "x.x.x.x"
}
```

### Get user-agent:

```bash
> http httpbin.org/user-agent

HTTP/1.1 200 OK
Access-Control-Allow-Credentials: true
Access-Control-Allow-Origin: *
Connection: keep-alive
Content-Length: 35
Content-Type: application/json
Date: Tue, 19 Sep 2017 03:39:45 GMT
Server: meinheld/0.6.1
Via: 1.1 vegur
X-Powered-By: Flask
X-Processed-Time: 0.000902891159058

{
    "user-agent": "HTTPie/0.9.9"
}
```

