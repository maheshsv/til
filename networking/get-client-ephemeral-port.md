# Get HTTP client ephemeral port

HTTP client doesn't need to bind to port because the client doesn't care about local IP address and the local port number. The TCP/IP stack within the kernel automatically assigns the local IP address and the local port when the client connect to server. The local port is called an ephemeral port, i.e. a short-lived port.

Make a client connection to the server and see what the ephemeral port kernel assigns to the socket(assume there is a HTTP server running on port 8888 of localhost).

```bash
>>> import socket
>>> sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
>>> sock.connect(('localhost', 8888))
>>> host, port = sock.getsockname()
>>> host, port
('127.0.0.1', 54702)
```

In this case the ephemeral port is 54702 to the socket.

From [Ruslan's Blog](https://ruslanspivak.com/lsbaws-part3/).
