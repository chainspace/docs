---
weight: 100
title: Performance Testing
---

# Performance Testing

## Consensus

The `chainspace genload <networkname> <nodenumber>` command starts up the specified node, and additionally a client which floods the consensus interface (in Go) with simulated transactions (100 bytes by default).

To get some consensus performance numbers, run this in 4 separate terminals:

```bash
rm -rf ~/.chainspace
chainspace init foonet
chainspace genload foonet 1
chainspace genload foonet 4
chainspace genload foonet 7
chainspace genload foonet 10
```

The client keeps increasing load until it detects that the node is unable to handle the transaction rate, based on timing drift when waking up to generate epochs. At that point the client backs off, and in general a stable equilibrium is reached. The `genload` console logs then report on average, current, and highest transactions per second throughput.

A convenient script runner is included. The short way to run it is:

```bash
rm -rf ~/.chainspace
chainspace init foonet
script/genload-testnet foonet
```

This will start nodes 1, 4, 7 and 10 in `tmux` terminals, pumping transactions through automatically.

<aside class="warning">To get valid results, turn off all other applications when doing performance testing. Also disable swap on your system, turn off CPI BIOS thermal controls, disable power management, and don't run it on battery power.</aside>



Running `chainspace genload` with swap enabled can cause system lockups on Linux, as the system thinks much more RAM is available than is in fact the case, write latencies increase drastically once swapping starts, and the system freaks out. `sudo swapoff -a` is your friend, with `sudo swapon -a` to get your swap back when you're done running Chainspace.

TODO: note what we see :).

## Sharding

[TODO: Jeremy's got some perf test scripts which we can document.]
