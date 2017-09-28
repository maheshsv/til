# Kong Admin API Models

### API Object

APIs exposed by Kong, each API object mush specify some combination of `hosts`, `uris` and `methods`.

```bash
{
    "created_at": 1488830759000,
    "hosts": [
        "example.org"
    ],
    "http_if_terminated": true,
    "https_only": false,
    "id": "6378122c-a0a1-438d-a5c6-efabae9fb969",
    "name": "example-api",
    "preserve_host": false,
    "retries": 5,
    "strip_uri": true,
    "upstream_connect_timeout": 60000,
    "upstream_read_timeout": 60000,
    "upstream_send_timeout": 60000,
    "upstream_url": "http://httpbin.org"
}
```

### Consumer Object

Consumer or user of APIs.

```bash
{
    "custom_id": "abc123"
}
```

### Plugin Object

Plugin configuration get executed during HTTP request/response workflow, Such as authorization, rate limiting.

```bash
{
    "id": "4d924084-1adb-40a5-c042-63b19db421d1",
    "api_id": "5fd1z584-1adb-40a5-c042-63b19db49x21",
    "consumer_id": "a3dX2dh2-1adb-40a5-c042-63b19dbx83hF4",
    "name": "rate-limiting",
    "config": {
        "minute": 20,
        "hour": 500
    },
    "enabled": true,
    "created_at": 1422386534
}
```

Four ways to add plugin:

- For every API and Consumer. Don't set `api_id` and `consumer_id`.
- For every API and a specific Consumer. Only set `consumer_id`.
- For every Consumer and a specific API. Only set `api_id`.
- For a specific Consumer and API. Set both `api_id` and `consumer_id`.


### Certificate Object

> A certificate object represents a public certificate/private key pair for an SSL certificate. These objects are used by Kong to handle SSL/TLS termination for encrypted requests. Certificates are optionally associated with SNI objects to tie a cert/key pair to one or more hostnames.

```bash
{
    "cert": "-----BEGIN CERTIFICATE-----...",
    "key": "-----BEGIN RSA PRIVATE KEY-----..."
}
```

### SNI Object

> An SNI object represents a many-to-one mapping of hostnames to a certificate. That is, a certificate object can have many hostnames associated with it; when Kong receives an SSL request, it uses the SNI field in the Client Hello to lookup the certificate object based on the SNI associated with the certificate.

```bash
{
    "name": "example.com",
    "ssl_certificate_id": "21b69eab-09d9-40f9-a55e-c4ee47fada68"
}
```

### Upstream Object

> The upstream object represents a virtual hostname and can be used to loadbalance incoming requests over multiple services (targets). So for example an upstream named `service.v1.xyz` with an API object created with an `upstream_url=https://service.v1.xyz/some/path`. Requests for this API would be proxied to the targets defined within the upstream.

```bash
{
    "name": "service.v1.xyz",
    "orderlist": [
        1,
        2,
        7,
        9,
        6,
        4,
        5,
        10,
        3,
        8
    ],
    "slots": 10
}
```

### Target Object

> A target is an ip address/hostname with a port that identifies an instance of a backend service. Every upstream can have many targets, and the targets can be dynamically added. Changes are effectuated on the fly.

```bash
{
    "target": "1.2.3.4:80",
    "weight": 15,
    "upstream_id": "ee3310c1-6789-40ac-9386-f79c0cb58432"
}
```

