A Go http streaming client. `http-streaming` is most-associated with the
Twitter Stream API.  This client works with [Twitter], but has also been tested
against the [DataSift] stream as well as [Flowdock].

[Twitter]: //twitter.com
[DataSift]: //datasift.com
[Flowdock]: //flowdock.com



This is an example of using the Twitter stream sample:

```go
package main

import "github.com/araddon/httpstream"

func main() {
	stream := make(chan []byte)
	done := make(chan bool)
	client := httpstream.NewBasicAuthClient("yourusername", "pwd", func(line []byte) {
		stream <- line
	})
	go func() {
		_ := client.Sample(done)
		for line := range stream {
			println(string(line))
			// heavy lifting like json serialization, etc
		}
	}()
	_ = <- done
}
```

There are a few more samples in the [examples] folder.

[examples]: tree/master/examples

Use a channel instead of `func`:

```go
stream := make(chan []byte)
done := make(chan bool)
client := httpstream.NewChannelClient("yourusername", "pwd", stream)
go func() {
	for line := range stream {
		println(string(line))
	}
}()
client.Sample(done)
_ = <- done
```

More information about streaming apis:

* [Twitter Stream API](//dev.twitter.com/docs/streaming-api/methods)
* [DataSift Stream API](//dev.datasift.com/docs/streaming-api)
* [Flowdock API](//www.flowdock.com/api)
