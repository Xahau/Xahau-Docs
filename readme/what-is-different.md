---
description: A list of notable differences between the XRP Ledger and Xahau.
---

# What is Different?

{% hint style="warning" %}
## Not Documented

* accounts on xahau start at a sequence that matches the timestamp of the previous ledger
* Pseudo tx docs missing: UNLReport, EmitFailure, Etc
* URIToken Size Limit
* AccountDelete is still listed as a transaction but is disabled on Xahau
{% endhint %}

#### IOU Token Escrow & PayChannels

Xahau introduces IOU Token Escrow and PayChannels as unique features, enhancing transaction flexibility and security. They facilitate the temporary holding of IOU tokens under predefined conditions (escrow) and the establishment of payment channels for efficient, off-ledger transactions.

{% content-ref url="../features/network-features/payments.md" %}
[payments.md](../features/network-features/payments.md)
{% endcontent-ref %}

#### URITokens NOT NFTokens

Instead of using NFTokens like XRPL, Xahau employs URITokens. URITokens are a form of non-fungible digital assets with unique identifiers and metadata, offering a novel approach to asset representation on the blockchain.

{% content-ref url="../features/network-features/uritoken.md" %}
[uritoken.md](../features/network-features/uritoken.md)
{% endcontent-ref %}

#### Different Repo

Xahau and XRPL operate from different repositories, signifying that they are separate protocols with their own development trajectories and documentation. This distinction implies that Xahau may offer unique features and optimizations not found in XRPL.

[https://github.com/Xahau/xahaud](https://github.com/Xahau/xahaud)

#### Different Build Process (WASM & LLVM)

Xahau's build process incorporates WebAssembly (WASM) and the Low-Level Virtual Machine (LLVM), which is not described in the XRPL build process. Xahau is utilizing these technologies for enhanced smart contract capabilities and to improve the performance and cross-platform compatibility of its codebase.

{% content-ref url="../infrastructure/building-xahau/" %}
[building-xahau](../infrastructure/building-xahau/)
{% endcontent-ref %}

#### Different Amendment Time (5 days)

The amendment process in Xahau has a specified time frame of 5 days, differing from XRPL's timeline. Amendments are protocol changes, and the 5-day period refers to the duration validators have to reach a consensus and implement these changes.

{% content-ref url="../features/amendments.md" %}
[amendments.md](../features/amendments.md)
{% endcontent-ref %}

#### Different Starting Sequence

Xahau employs a different starting sequence for accounts than XRPL. The initial sequence on the account is the ripple epoch time when the account was create/imported into Xahau.

#### Import / Burn 2 Mint

Importing from XRPL to Xahau grants users 2 XAH tokens, indicating an incentive mechanism to encourage asset migration or bridging from XRPL to Xahau, potentially to enhance network adoption and liquidity.

{% content-ref url="../technical/burn-2-mint.md" %}
[burn-2-mint.md](../technical/burn-2-mint.md)
{% endcontent-ref %}

#### Balance Rewards (Rewards for using XAH)

Xahau offers balance rewards for utilizing XAH, a feature absent in XRPL. This is a reward system for holding or using Xahau's native token, XAH, to promote network engagement and stability.

{% content-ref url="../features/network-features/balance-rewards.md" %}
[balance-rewards.md](../features/network-features/balance-rewards.md)
{% endcontent-ref %}

#### Hooks

Hooks in Xahau, which are not present in XRPL, are programmable scripts or smart contract-like functions that can be attached to accounts. They add a layer of programmability and automation to the network's operations.

{% content-ref url="../readme-1.md" %}
[readme-1.md](../readme-1.md)
{% endcontent-ref %}

#### Governance Structure

Xahau's governance structure differs from XRPL's. Xahau has its own approach to decision-making, proposal systems, or validator roles, which could influence the network's evolution.

{% content-ref url="../technical/governance-game.md" %}
[governance-game.md](../technical/governance-game.md)
{% endcontent-ref %}

#### Node Requirements

Running a Xahau node has different requirements compared to an XRPL node. These differences could be related to the technical specifications needed to support Xahau's unique features and network demands.

{% content-ref url="../infrastructure/node-requirements.md" %}
[node-requirements.md](../infrastructure/node-requirements.md)
{% endcontent-ref %}

#### Native Token

Xahau's native token is XAH, distinct from XRPL's XRP. As the primary currency within the Xahau network, XAH likely serves as the main medium of exchange and a store of value, central to the network's economic framework.

{% content-ref url="../technical/protocol-reference/data-types/currency-formats.md" %}
[currency-formats.md](../technical/protocol-reference/data-types/currency-formats.md)
{% endcontent-ref %}

#### Versioning (Uses Dates)

Xahau employs a date-based versioning system, unlike XRPL's versioning approach. This method may provide a more intuitive means of tracking the network's updates and historical development.

{% content-ref url="../technical/versioning-process.md" %}
[versioning-process.md](../technical/versioning-process.md)
{% endcontent-ref %}
