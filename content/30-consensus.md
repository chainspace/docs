---
weight: 30
title: Consensus
---

# Consensus

## Introduction

TODO: what is consensus anyway? Why do we need it?

## Sending Transactions To Consensus

At the moment, there is no externally-exposed network interface for using the consensus component by itself. You can however access it programmatically using Go, e.g.

> Sending data to consensus whne you have compiled a client. This only works in Go. 

```go
import "chainspace.io/prototype/node"

s, err := node.Run(cfg)
if err != nil {
  log.Fatal(err)
}
s.Broadcast.AddTransaction(txdata, fee)
```

[DAVE TODO: check that the above code can actually run]

[TODO: build out a Blockmania HTTP API endpoint that can accept transactions and order them]

[TODO: let's build a separate Blockmania binary that can be run independently, and keep its configs in `~/.blockmania/{networkname}`]
