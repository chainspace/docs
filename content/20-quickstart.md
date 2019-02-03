---
weight: 20
title: Quickstart
---

# Quickstart

## Installation

* Install Go 1.11. Earlier versions won't work.
* Install `tmux`
* `git clone` the code into `$GOPATH`, typically `~/go/src/chainspace.io/prototype`
* `make install` will install to `$GOPATH/bin/chainspace`. Make sure this location is on your path.
* `make contract`

If everything worked, the `chainspace` command should be installed and available. Running it will give an overview of available functionality. Help flags are available, have a look.

## Initialize a network

The `chainspace init {networkname}` command, by default, creates a network consisting of 12 nodes grouped into 3 shards of 4 nodes each.

> Initialize a new Chainspace network called "foonet"

```
chainspace init foonet
```

The setup you get from that is heavily skewed towards convenient development rather than production use. It will change as we get closer to production.

Have a look at the config files for the network you've generated (stored by default in `~/.chainspace/{networkname}`). The `network.yaml` file contains public signing keys and transport encryption certificates for each node in the network. Everything in `network.yaml` is public, and for the moment it defines network topology. Later, it will be replaced by a directory component.

Each node also gets its own named configuration directory, containing:

* public and private signing and transport encryption keys for each node
* a node configuration file
* log output for the node

## Running nodes

In the default localhost setup, nodes `1`, `4`, `7`, and `10` comprise shard 1. Run those node numbers if you're only interested in seeing consensus working. Otherwise, start all nodes to see sharding working as well.

> Here's how you can init a network and start each node individually

```bash
make contract # you only need to do this once, it installs a dummy Docker contract
chainspace contracts foonet create # you only need to do this once, it links the Docker contract to your nodes
rm -rf ~/.chainspace/foonet
chainspace init foonet
chainspace run foonet 1
chainspace run foonet 4
chainspace run foonet 7
chainspace run foonet 10
```

> A convenient script runner is included. The short way to run it is

```bash
make contract # you only need to do this once, it installs a dummy Docker contract
chainspace contracts foonet create # you only need to do this once, it links the Docker contract to your nodes
rm -rf ~/.chainspace/foonet
chainspace init foonet
script/run-testnet foonet
```

This will fire up a single shard which runs consensus, and make it available for use.

## REST documentation

Many parts of the system are available to poke at via a RESTful HTTP server interface. After starting a node locally, you can see what's available by going to http://localhost:9001/swagger/index.html - where `9001` is the node's HTTP server port as defined in `~/.chainspace/{networkname}/node-{nodenumber}/node.yaml`. In the default generated config, REST port number is http://localhost:{9000+nodenumber} for each node.
