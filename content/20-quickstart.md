---
weight: 20
title: Quickstart
---

# Quickstart

* Install Go 1.11. Earlier versions won't work.
* `git clone` the code into the source dir of your `$GOPATH`, typically `~/go/src`
* `make install`
* `make contract`

### Setting Up and Running Nodes

The `chainspace init <networkname>` command, by default, creates a network consisting of 12 nodes grouped into 3 shards of 4 nodes each.

The setup you get from that is heavily skewed towards convenient development rather than production use. It will change as we get closer to production.

Have a look at the config files for the network you've generated (stored by default in `~/.chainspace/<networkname>`). The `network.yaml` file contains public signing keys and transport encryption certificates for each node in the network. Everything in `network.yaml` is public, and for the moment it defines network topology. Later, it will be replaced by a directory component.

Each node also gets its own named configuration directory, containing:

* public and private signing and transport encryption keys for each node
* a node configuration file
* log output

In the default setup, nodes 1, 4, 7, and 10 comprise shard 1. Run those node numbers if you're only interested in seeing consensus working. Otherwise, start all nodes to see sharding working as well.

```bash
rm -rf ~/.chainspace # destroy any old configs, make you sad in production
chainspace init foonet
chainspace run foonet 1
chainspace run foonet 4
chainspace run foonet 7
chainspace run foonet 10
```

A convenient script runner is included. The short way to run it is:

```bash
rm -rf ~/.chainspace # clear previous configs, superbad idea in production
chainspace init foonet
script/run-testnet foonet
```

This will fire up a single shard which runs consensus, and make it available for use.

## REST Documentation

Many parts of the system are available to poke at via a RESTful HTTP server interface. After starting a node locally, you can see what's available by going to http://localhost:9001/swagger/index.html - where `9001` is the node's HTTP server port as defined in `~/.chainspace/<network-name>/node-X/node.yaml`
