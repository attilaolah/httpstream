## To run examples:

```bash
go run jsonmarshall.go
```

A valid twitter username/pwd will get sample stream:

```bash
go run simple.go -user=myusername -pwd=mypwd
```

For flowdock.com

```
go run flowdock.go -token=x3456 -flow=myorg/main
```

Send to zeromq (sink is the zmq address to bind to:  downstream can subscribe):

```bash
go get github.com/alecthomas/gozmq
go run zmq.go -user=myusername -pwd=mypwd  --sink=tcp://*:5555
```
