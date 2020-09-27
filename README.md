hdfseeder
=========

[![Build Status](https://github.com/hdfchain/hdfseeder/workflows/Build%20and%20Test/badge.svg)](https://github.com/hdfchain/hdfseeder/actions)
[![ISC License](https://img.shields.io/badge/license-ISC-blue.svg)](http://copyfree.org)

## Overview

hdfseeder is a crawler for the Hdfchain network, which exposes a list of reliable
nodes via a built-in HTTP server.

When hdfseeder is started for the first time, it will connect to the hdfd node
specified with the `-s` flag, send a `getaddrs` request, expecting an  `addr`
message response. This message contains hostnames and IPs of peers known by the
node. hdfseeder will then connect to each of these peers, send a `getaddrs`
request, and will continue traversing the network in this fashion. hdfseeder
maintains a list of all known peers and periodically checks that they are
online and available. The list is stored on disk in a json file, so on
subsequent start ups the hdfd node specified with `-s` does not need to be
online.

When hdfseeder is queried for node information, it responds with details of a
random selection of the reliable nodes it knows about.

## Requirements

[Go](https://golang.org) 1.12 or newer.

### Getting Started

To build and install from a checked-out repo, run `go install` in the repo's
root directory.

To start hdfseeder listening on udp 127.0.0.1:5354 with an initial connection to working testnet node 192.168.0.1:

```no-highlight
$ ./hdfseeder -s 192.168.0.1 --testnet --httplisten=localhost:8000
```

You will then need to redirect HTTPS traffic on your public IP to localhost:8000

For more information about Hdfchain and how to set up your software please go to
our docs page at [docs.clkj.ltd](https://docs.clkj.ltd/getting-started/beginner-guide/).

## Issue Tracker

The [integrated github issue tracker](https://github.com/hdfchain/hdfseeder/issues)
is used for this project.

## License

hdfseeder is licensed under the [copyfree](http://copyfree.org) ISC License.
