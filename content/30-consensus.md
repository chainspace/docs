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

## Sending transactions

At the moment, there is no externally-exposed network interface for using the consensus component by itself. You can however access it programmatically using Go.

> Sending data to consensus whne you have compiled a client. This only works in Go.

```go
import "chainspace.io/prototype/node"

s, err := node.Run(cfg)
if err != nil {
  log.Fatal(err)
}
s.Broadcast.AddTransaction(txdata, fee)

```
[TODO: check that the above code can actually run]


## Using REST


[TODO: build out a Blockmania HTTP API endpoint that can accept transactions and order them]

[TODO: let's build a separate Blockmania binary that can be run independently, and keep its configs in `~/.blockmania/{networkname}`]
