---
weight: 30
title: Consensus
---

# Consensus

## Introduction

Consensus algorithms allow nodes in a distributed system to agree on a specific **order of transactions** without a central authority.

Incoming transactions arrive at nodes in an arbitrary order, potentially even at the same time. Participating nodes then talk to each other, and agree on an ordering of transactions which is **guaranteed to be the same** for all of them.

Blockmania is a [Byzantine Fault Tolerant](https://en.wikipedia.org/wiki/Byzantine_fault_tolerance) consensus algorithm. It functions correctly even if 1/3 participants are faulty or actively acting as attackers, with no loss of liveness or safety. In conditions where more than 1/3 of nodes are bad, Blockmania prioritises safety over liveness. Attackers or faulty nodes can stop processing for the cluster, but they cannot inject bad data.

Blockmania nodes group incoming transactions into blocks, and exchange signed data and witness statements which are then propagated to all participating nodes. Each node writes out the same signed sequence of blocks, or blockchain, as every other node participating in a given consensus group. A chain of concatenated block hashes ensures that data cannot be arbitrarily changed by any participating nodes, even dishonest ones.

If you're curious about how it works at a deeper level, please read the [Blockmania](https://arxiv.org/abs/1809.01620) academic paper.

The Chainspace codebase builds Blockmania into itself, but doesn't expose any network interface for sending transactions. If you're a Go coder, you can however access it programmatically using Go, something like this:

> Sending data to consensus whne you have compiled a client. This only works in Go.

```go
import "chainspace.io/chainspace-go/node"

s, err := node.Run(cfg)
if err != nil {
  log.Fatal(err)
}
s.Broadcast.AddTransaction(txdata, fee)

```

## Using Blockmania by itself

It is also possible to use Blockmania by itself.

1. Clone the Blockmania repo
1. Run `make install`
1. Run ` blockmania init -network-name foomania`

This will generate, by default, a 4-node Blockmania network. Config files are at `~/.blockmania/foomania`. Each node gets its own separate configuration.

You can run each node (1-4) by doing:

`blockmania run -network-name foomania -node-id 1`
`blockmania run -network-name foomania -node-id 2`
`blockmania run -network-name foomania -node-id 3`
`blockmania run -network-name foomania -node-id 4`

For development purposes, there's also `scripts/run-testnet` which will generate a testnet and run it in a `tmux`.

## Using REST

Each Blockmania node starts a REST API by default. Docs are available at http://localhost:8001 (for node 1, each successive node increments the port number by 1).

Swagger docs are available at http://localhost:8001/swagger/index.html

## Subscribing to Blockmania events

You should be able to see the websocket routes in the included Swagger documentation on each node (although you won't be able to try it out as our Swagger server doesn't support websockets). For standalone Blockmania, the websockets server(s) start on http://localhost:7001/api/pubsub/ws (for node 1, each successive node increment the port number by 1).

Socket.io websockets don't work, as they're incompatible with the Go websocket implementation we're using. Other websockets should work.

Alternately, you can use the `pubsublistener`, a Go utility we've included for you to watch events as they happen. It works like this:

`pubsublistener -addrs 1=localhost:7001,2=localhost:7002,3=localhost:7003,4=localhost:7004`

Try sending a transaction like this one through the `POST /api/transaction` endpoint in Swagger:

```
{
  "tx": [
    1
  ]
}
```

You should see the `pubsublistener` print out the Base64-encoded value of your input a few seconds after you send it. 
