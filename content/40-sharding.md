---
weight: 40
title: Sharding
---

# Sharding

## Introduction

Chainspace allows multiple Blockmania blockchains to talk to each other. Each grouping of Blockmania nodes becomes a Chainspace *shard*. Shards can operate independently of each other, so the system as a whole can scale horizontally and benefit from parallelism. Chainspace is a protocol which coordinates operations across more than one shard. Crucially, operations are atomic across shards: a transaction touching multiple contracts in multiple shards will either succeed or fail in its entirety.

## Architectural overview

There are a few different moving parts:

1. Clients
1. Contracts
1. Checkers

The basic application flow is as follows:

1. The **client** sends information to a **contract** as a network request (currently implemented as a REST service). The contract checks its local datastore, and returns a transaction.
1. The client sends the transaction to all nodes in the shard. Each node runs a **checker** on the transaction; the checker validates the transaction against the current state of the chain, signs the transaction and returns it.
1. The client bundles up all the transaction signatures, and sends the bundled signatures and transaction data to one of the nodes in the shard. If more than 2/3 of nodes agreed that the transaction is valid, the transaction is then sequenced into the blockchain.
1. Clients may subscribe to the blockchain to receive speedy notifications of updates.

Clients, contracts, and checkers can be implemented in any language.

### Clients and client libraries

Client libraries exist in multiple languages, and we're in the process of writing more. Please let us know if you're interested in contributing a client in your favourite language.


### Contracts

### Checkers

### Emulator



## Sending transactions

TODO. Stu's got a transaction we can use now I think.

This will be where we introduce the idea of different clients for each language. We can make that point first (hopefully to reduce cognitive load on our users). But later, we can detail how the whole process works, so people can develop their own clients in languages we don't yet support.

## Using clients

## Using REST

## Determinism
