---
weight: 10
title: Introduction
---

# Introduction

Chainspace is a smart contract platform offering speedy consensus and unlimited horizontal scalability. Our goal is to build a blockchain platform that scales like the web scales: adding machines should increase overall capacity, and there should be no built-in scalability limitations.

At present, our running code has two main components:

* `blockmania` is a consensus component. It implements the leaderless consensus protocol detailed in the [Blockmania](https://arxiv.org/abs/1809.01620) academic paper. It takes transactions to any participating node as input, and outputs an immutable and deterministic total ordering of transactions. Each set of Blockmania nodes produces an immutable blockchain.
* `chainspace` is a sharding component. It provides an implementation of the Sharded Byzantine Atomic Commit (SBAC) protocol detailed in the [Chainspace](https://arxiv.org/abs/1708.03778) academic paper. Within the overall Chainspace system, each Blockmania blockchain acts as a shard, and SBAC enables cross-shard transactions.

Eventually, it's likely that we will split these two components. A project wanting only fast consensus, but no sharding, should be able use Blockmania by itself. For projects that need the added horizontal scalability of sharding, the Chainspace component would be added. However, for the moment, the two components co-exist in the same codebase.
