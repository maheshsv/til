# DNS: The Good Part Notes

Notes from the [post](https://www.petekeen.net/dns-the-good-parts).

### What is DNS?

> Domain Name System, globaly distributed key value store.

Look at a domain name to IP address mapping with `dig`, a DNS lookup utility.

```bash
$ dig web01.bugsplat.info

; <<>> DiG 9.8.3-P1 <<>> web01.bugsplat.info
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 48341
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;web01.bugsplat.info.       IN  A

;; ANSWER SECTION:
web01.bugsplat.info.    300 IN  A   192.241.250.244

;; Query time: 182 msec
;; SERVER: 75.75.75.75#53(75.75.75.75)
;; WHEN: Wed Jun 22 21:28:23 2016
;; MSG SIZE  rcvd: 53
```

`dig` defaults to asking for `A` record.

Run a trace too see all of the servers `dig` would have to contact if they weren't already cached.

```bash
$ dig +trace web01.bugsplat.info

; <<>> DiG 9.8.3-P1 <<>> +trace web01.bugsplat.info
;; global options: +cmd
.           464733  IN  NS  h.root-servers.net.
.           464733  IN  NS  g.root-servers.net.
.           464733  IN  NS  i.root-servers.net.
.           464733  IN  NS  m.root-servers.net.
.           464733  IN  NS  c.root-servers.net.
.           464733  IN  NS  b.root-servers.net.
.           464733  IN  NS  a.root-servers.net.
.           464733  IN  NS  k.root-servers.net.
.           464733  IN  NS  d.root-servers.net.
.           464733  IN  NS  l.root-servers.net.
.           464733  IN  NS  f.root-servers.net.
.           464733  IN  NS  e.root-servers.net.
.           464733  IN  NS  j.root-servers.net.
;; Received 508 bytes from 75.75.75.75#53(75.75.75.75) in 262 ms

info.           172800  IN  NS  b0.info.afilias-nst.org.
info.           172800  IN  NS  a0.info.afilias-nst.info.
info.           172800  IN  NS  c0.info.afilias-nst.info.
info.           172800  IN  NS  b2.info.afilias-nst.org.
info.           172800  IN  NS  a2.info.afilias-nst.info.
info.           172800  IN  NS  d0.info.afilias-nst.org.
;; Received 440 bytes from 192.36.148.17#53(192.36.148.17) in 1149 ms

bugsplat.info.      86400   IN  NS  ns-212.awsdns-26.com.
bugsplat.info.      86400   IN  NS  ns-911.awsdns-49.net.
bugsplat.info.      86400   IN  NS  ns-1356.awsdns-41.org.
bugsplat.info.      86400   IN  NS  ns-1580.awsdns-05.co.uk.
;; Received 177 bytes from 199.249.113.1#53(199.249.113.1) in 119 ms

web01.bugsplat.info.    300 IN  A   192.241.250.244
bugsplat.info.      172800  IN  NS  ns-1356.awsdns-41.org.
bugsplat.info.      172800  IN  NS  ns-1580.awsdns-05.co.uk.
bugsplat.info.      172800  IN  NS  ns-212.awsdns-26.com.
bugsplat.info.      172800  IN  NS  ns-911.awsdns-49.net.
;; Received 193 bytes from 205.251.198.44#53(205.251.198.44) in 154 ms
```

Reverse lookup the root server domain name:

```bash
$ dig -x 192.36.148.17

; <<>> DiG 9.8.3-P1 <<>> -x 192.36.148.17
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 44970
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;17.148.36.192.in-addr.arpa.    IN  PTR

;; ANSWER SECTION:
17.148.36.192.in-addr.arpa. 86400 IN    PTR i.root-servers.net.

;; Query time: 1005 msec
;; SERVER: 75.75.75.75#53(75.75.75.75)
;; WHEN: Wed Jun 22 21:51:48 2016
;; MSG SIZE  rcvd: 76
```

The host of the random root server is `i.root-servers.net.`.

### Other types of record

`MX`: domain name to email servers.

```bash
$ dig petekeen.net mx

; <<>> DiG 9.8.3-P1 <<>> petekeen.net mx
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 29221
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;petekeen.net.          IN  MX

;; ANSWER SECTION:
petekeen.net.       3600    IN  MX  10 in1-smtp.messagingengine.com.
petekeen.net.       3600    IN  MX  20 in2-smtp.messagingengine.com.

;; Query time: 124 msec
;; SERVER: 75.75.75.75#53(75.75.75.75)
;; WHEN: Wed Jun 22 22:00:45 2016
;; MSG SIZE  rcvd: 99
```

Note that `MX` record points to a name and not an IP address.

`CNAME`: Canonical Name, maps one name onto another.

```bash
$ dig www.petekeen.net

; <<>> DiG 9.8.3-P1 <<>> www.petekeen.net
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 15047
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;www.petekeen.net.      IN  A

;; ANSWER SECTION:
www.petekeen.net.   86400   IN  CNAME   web02.bugsplat.info.
web02.bugsplat.info.    300 IN  A   54.173.164.4

;; Query time: 175 msec
;; SERVER: 75.75.75.75#53(75.75.75.75)
;; WHEN: Wed Jun 22 22:01:40 2016
;; MSG SIZE  rcvd: 83
```

Query specific server:

```bash
$ dig www.petekeen.net @8.8.8.8
```

Most DNS servers allow you to set up DNS wildcards. Such as `*.web01.bugsplat.info`.


### RFCs

The Internet standards define DNS are:

- [RFC 1034: Domain Names - Concepts and Facilities](http://www.ietf.org/rfc/rfc1034.txt)
- [RFC 1035: Domain Names - Implementation and Specification](http://www.ietf.org/rfc/rfc1035.txt)
