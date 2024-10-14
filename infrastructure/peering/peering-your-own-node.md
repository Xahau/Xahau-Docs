---
description: >-
  Xahau Testnet allows for running your own local node. You can run a Docker
  Container or connect with your own local running instance.
---

# Running a Testnet Node

### Connecting to the Xahau Testnet with Docker

To connect to the Xahau Testnet (Hooks V3 testnet) you can use this Docker container:

{% embed url="https://github.com/Xahau/Xahau-Testnet-Docker/" %}

1. Clone the repository
2. Run `./build`
3. Run `./up`
4. Check the README for commands, etc.\
   [https://github.com/Xahau/Xahau-Testnet-Docker/blob/main/README.md](https://github.com/Xahau/Xahau-Testnet-Docker/blob/main/README.md)
5. Connect using WebSockets or RPC:\
   WebSocket: `ws://localhost:16006`\
   RPC (HTTP POST): `http://localhost:16007`

## Local instance

### Peering info

<table data-header-hidden><thead><tr><th width="181"></th><th></th></tr></thead><tbody><tr><td>Info &#x26; Faucet</td><td><a href="https://xahau-test.net/">https://xahau-test.net</a></td></tr><tr><td>Explorer</td><td><a href="https://explorer.xahau-test.net/">https://explorer.xahau-test.net</a></td></tr><tr><td>Technical docs</td><td><a href="https://xrpl-hooks.readme.io/">https://xrpl-hooks.readme.io</a></td></tr><tr><td>WebSocket URL</td><td><a href="https://xahau-test.net/">wss://xahau-test.net</a></td></tr><tr><td>Public peering</td><td>Network ID: <strong><code>21338</code></strong><br><br>Peer 1: <code>68.183.1.245</code> Port: 21338<br>Peer 2: <code>159.65.199.56</code> Port: 21338<br>Peer 3: <code>139.59.98.59</code> Port: 21338<br>Peer 4: <code>79.110.60.122</code> Port: 21338<br>Peer 5: <code>79.110.60.124</code> Port: 21338<br>Peer 6: <code>79.110.60.125</code> Port: 21338<br>Peer 7: <code>79.110.60.121</code> Port: 21338</td></tr><tr><td>Binary &#x26; config</td><td><p>For ubuntu 22.04:<br><br><strong>Download:</strong></p><p><a href="https://build.xahau.tech/2023.9.25-dev%2B336"><strong>https://build.xahau.tech/2023.9.25-dev%2B336</strong></a></p><p><br>Extract, then run: <br><code>./xahaud --net --quorum=5 --conf xahaud.cfg</code> Config file sample (to be saved as <code>xahaud.cfg</code>):</p><ul><li><p><a href="https://github.com/Xahau/Xahau-Testnet-Docker/blob/main/store/etc/xahaud.cfg">https://github.com/Xahau/Xahau-Testnet-Docker/blob/main/store/etc/xahaud.cfg</a></p><ul><li>Edit the database path, etc if needed.</li></ul></li><li>In the same folder as the <code>xahaud.cfg</code> config, the <code>validators-xahau.txt</code> file should be stored:<br><br><a href="https://github.com/Xahau/Xahau-Testnet-Docker/blob/main/store/etc/validators-xahau.txt">https://github.com/Xahau/Xahau-Testnet-Docker/blob/main/store/etc/validators-xahau.txt</a></li></ul></td></tr><tr><td>Validators</td><td><code>[validators]</code><br><code>nHDs6fHVnhb4ZbSFWF2dTTPHoZ6Rr39i2UfLotzgf8FKUi7iZdxx nHUvgFxT8EGrXqQZ1rqMw67UtduefbaCHiVtVahk9RXDJP1g1mB4 nHU7Vn6co7xEFMBesV7qw7FXE8ucKrhVWQiYZB5oGyMhvqrnZrnJ nHBoJCE3wPgkTcrNPMHyTJFQ2t77EyCAqcBRspFCpL6JhwCm94VZ nHUVv4g47bFMySAZFUKVaXUYEmfiUExSoY4FzwXULNwJRzju4XnQ nHBvr8avSFTz4TFxZvvi4rEJZZtyqE3J6KAAcVWVtifsE7edPM7q nHUH3Z8TRU57zetHbEPr1ynyrJhxQCwrJvNjr4j1SMjYADyW1WWe</code></td></tr></tbody></table>



### Integrating Xumm with Hooks V3

<figure><img src="../../.gitbook/assets/image.png" alt="" width="145"><figcaption></figcaption></figure>

To connect Xumm to the Hooks V3 staging net, scan this QR with the QR scanner in Xumm to add the endpoint (above) to the Xumm node list.
