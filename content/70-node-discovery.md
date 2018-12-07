---
weight: 70
title: Node Discovery
---

# Node Discovery

So far, this documentation has assumed that all nodes are running on a single machine. What if you want to run each node on a separate machine on a local network, or across the internet?

We have not yet implemented seed nodes, or a cryptographically secure method of peer discovery. So we have implemented some simple methods for stitching together networks until we are ready to commit to a final system.

Nodes currently find each other in two ways:

1. mDNS discovery
1. registry

## mDNS discovery

In development or on private networks, nodes can discover each other using mDNS broadcast. This allows zero-configuration setups for nodes that are all on the same subnet.

## Registry

Use the Registry when configuring nodes across the public internet. We run a public registry at https://registry.chainspace.io.

You can run your own Registry if you want. Init your network with the `--registry` flag if you plan to use a Registry server:

```bash
chainspace init foonet --registry registry.chainspace.io
```

The Registry will then appear in each node's `node.yaml`:

```yaml
registries:
- host: registry.chainspace.io
- token: 05b16f5d45377baff52c25e2c154a00b126f7b75b7345794d3e15535b49a03f955b9c355
```

The randomly-generated registry `token` ensures that a unique shared secret is used on a per-network basis so that multiple networks can share the same registry without any additional setup.

Nodes will automatically register themselves with the network's registry server when they start up.

It is possible to use both the Registry and mDNS discovery at the same time, and have a sort of mixed network in operation.
