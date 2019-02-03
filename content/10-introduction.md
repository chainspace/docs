---
weight: 10
title: Introduction
---

# Introduction

Chainspace is a smart contract platform offering speedy consensus and unlimited horizontal scalability. Our goal is to build a blockchain platform that scales like the web scales: adding machines should increase overall capacity, and there should be no built-in scalability limitations.

At present, our running code has two main components:

* `blockmania` is a consensus component. It implements the leaderless consensus protocol detailed in the [Blockmania](https://arxiv.org/abs/1809.01620) academic paper. It takes transactions to any participating node as input, and outputs an immutable and deterministic total ordering of transactions. Each set of Blockmania nodes produces an immutable blockchain.
* `chainspace` is a sharding component. It provides an implementation of the Sharded Byzantine Atomic Commit (SBAC) protocol detailed in the [Chainspace](https://arxiv.org/abs/1708.03778) academic paper. Within the overall Chainspace system, each Blockmania blockchain acts as a shard, and SBAC enables cross-shard transactions. You should use the Go implementation at https://github.com/chainspace/chainspace-go.

Originally, both of these components existed within the same Go codebase. As of this writing, we are halfway between splitting these two components, so Blockmania exists in two places:

* the https://github.com/chainspace/blockmania repo
* the https://github.com/chainspace/chainspace-go repo (where it's built into the project)

A project wanting only fast consensus, but no sharding, should be able use Blockmania by itself. For projects that need the added horizontal scalability of sharding, the Chainspace component would be added. From a platform development point of view, getting a build working with the extracted Blockmania codebase in the `blockmania` repo is a big priority. But at least this way you can use Blockmania on its own, if that's what you want.
