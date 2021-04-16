
# TCPDump

Spy on eth0 interface for SSH packets going to my amazing server.

```
tcpdump -i eth0 host lupusmic.org and tcp port not 22
```

# Listen raw socket

Open a socket and listen to TCP client on `localhost`

```
nc -l 8080
```
