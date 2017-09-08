# Proxy Network

>  Proxy network/server acts as an intermediary for requests from clients seeking resources from other servers.

- forward proxy: an **Internet-facing** proxy used to retrieve from a wide range of sources (in most cases anywhere on the Internet).
- reverse proxy: usually an **internal-facing proxy** used as a front-end to control and protect access to a server on a private network. A reverse proxy commonly also performs tasks such as load-balancing, authentication, decryption or caching.

[luminati](https://luminati.io/) is one of the proxy network service providers. And it's very easy to use, an example is like:

```bash
> curl --proxy zproxy.luminati.io:22225 --proxy-user <username>:<password> "http://lumtest.com/myip.json"

```

