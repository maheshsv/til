# SSH Bind Address

### command

```bash
# local forwarding
ssh -L [bind_address:]port:host:hostport

# remote forwarding
ssh -R [bind_address:]port:host:hostport
```

### Examples

**local forwarding**

```bash
ssh -L 80:example.com:80
```

Forward conneciton to port 80 on localhost to port 80 on `example.com`.

**Remote forwarding**

```bash
ssh -R 8080:localhost:80 public.example.com
```

Connection to port 8080 on remote host will tunneled back to localhost 80.



Refer to [SSH Port Forwarding Example](https://www.ssh.com/ssh/tunneling/example).

