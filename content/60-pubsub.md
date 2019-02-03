---
weight: 60
title: Pubsub
---

# Pubsub

Interested clients can receive streaming notifications of changes to the blockchain through either websockets or raw TCP sockets.

This allows developers to:

* react immediately to changes with low latency
* stream changes to any datastore when query complexity is greater than what the built-in key-value store can provide.

## Websockets

`--enable-websockets`

`chainspace footest --shard-count 1 --enable-pubsub true`

You should be able to see the websocket routes in the included Swagger documentation on each node (although you won't be able to try it out as our Swagger server doesn't support websockets).

Assuming you're connecting on the first node on your local machine, you can make a websocket connection:

```html
<script>
   var ws = new WebSocket("ws://0.0.0.0:9001/api/pubsub/ws");
   ws.onmessage = function (event) {
       console.log(event.data);
   }
</script>
```

## TCP sockets

Port {7000 + nodenumber} by default (increments with the nodenumber). You can specify the port
