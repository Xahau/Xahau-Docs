---
description: >-
  Xahau Mainnet allows for running your own local node. You can run a Docker
  Container or connect with your own local running instance.
---

# Running a Mainnet Node

### Connecting to the Xahau Mainnet with Docker

To connect to the Xahau Mainnet you can use this docker container:

{% embed url="https://github.com/Xahau/mainnet-docker" %}

1. Clone the repository
2. Run `./build`
3. Run `./up`
4. Check the README for commands, etc. [https://github.com/Xahau/mainnet-docker/blob/main/README.md](https://github.com/Xahau/mainnet-docker/blob/main/README.md)
5. Connect using WebSockets or RPC:\
   WebSocket: `ws://localhost:16006`\
   RPC (HTTP POST): `http://localhost:16007`

## Local instance

### Peering info

<table data-header-hidden><thead><tr><th width="181"></th><th></th></tr></thead><tbody><tr><td>Info</td><td><a href="https://xahau.network/">https://xahau.network/</a></td></tr><tr><td>Explorer</td><td><a href="https://explorer.xahau.network/">https://explorer.xahau.network/</a></td></tr><tr><td>Technical docs</td><td><a href="https://xrpl-hooks.readme.io/">https://xrpl-hooks.readme.io</a></td></tr><tr><td>WebSocket URL</td><td><a href="wss://xahau.network">wss://xahau.network</a></td></tr><tr><td>Public peering</td><td>Network ID: <strong><code>21337</code></strong><br>Peer 1: bacab.alloy.ee 21337</td></tr><tr><td>Binary &#x26; config</td><td><p>For ubuntu 22.04:<br><br><strong>Download:</strong></p><p><a href="https://build.xahau.tech"><strong>https://build.xahau.tech</strong></a></p><p></p><p>For the latest release build numbers, see the <a href="https://github.com/Xahau/xahaud/actions?query=branch%3Arelease+is%3Asuccess+build+using+docker"><strong>Github Build Actions</strong></a>.</p><p><br>Extract, then run:<br><code>./xahaud --net --conf xahaud.cfg</code> Config file sample (to be saved as <code>xahaud.cfg</code>):</p><ul><li><p><a href="https://github.com/Xahau/mainnet-docker/blob/main/store/etc/xahaud.sample.cfg">https://github.com/Xahau/mainnet-docker/blob/main/store/etc/xahaud.cfg</a></p><ul><li>Edit the database path, etc if needed.</li></ul></li><li>In the same folder as the <code>xahaud.cfg</code> config, the <code>validators-xahau.txt</code> file should be stored:<br><br><a href="https://github.com/Xahau/mainnet-docker/blob/main/store/etc/validators-xahau.sample.txt">https://github.com/Xahau/mainnet-docker/blob/main/store/etc/validators-xahau.txt</a></li></ul></td></tr><tr><td>UNL (VL)</td><td><a href="https://vl.xahau.org/">https://vl.xahau.org/</a></td></tr></tbody></table>
