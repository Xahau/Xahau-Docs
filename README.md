---
description: >-
  Introducing Hooks: Enhancing XRP Ledger Protocol with Smart Contract
  Functionality
cover: .gitbook/assets/cdn.feather.webp
coverY: 0
---

# 🪝 Hooks

{% hint style="info" %}
Hooks are small, efficient WebAssembly modules designed specifically for the XRPL. They could be referred to as **Smart Contracts for the XRP Ledger Protocol**.

Hooks can be written in any language (compilable with WebAssembly), and most business logic and smart contract concepts can be implemented in a hook.

[**Development by XRPL Labs**](https://xrpl-labs.com/#team)
{% endhint %}

### What are Hooks? <a href="#what-are-hooks" id="what-are-hooks"></a>

Hooks allow the creation of customized logic and automation within the XRPL, making transactions smarter and more convenient. These small, efficient modules add custom on-ledger functionality, such as creating custom triggers for specific events on the ledger.&#x20;

These triggers can be used to send on-ledger actions or execute other actions in response to the specified event. Hooks are currently only available on the [XRPL Labs public Hooks testnet,](https://hooks-testnet-v2.xrpl-labs.com/) as the feature is under development.

> _There is a_ [_Hooks Builder site_](https://hooks.xrpl.org/) _where you can develop, test, debug, and deploy your own Hooks on testnet in your browser, using our examples or building your own from scratch._

### Why are Hooks a Big Deal? <a href="#why-are-hooks-a-big-deal" id="why-are-hooks-a-big-deal"></a>

Simply put, Hooks add a robust smart contract functionality to the XRPL, empowering you to construct and deploy applications with bespoke functionalities aligning with your specific needs and requirements.

Hooks provide a versatile platform as they can be used for implementing a broad spectrum of business logic and smart contract paradigms. Once a hook is set up on an account, it enables you to do the following:

* Block or allow transactions to and from the account.
* Change and keep track of the hook’s internal state and logic to inform programmatic choices.
* Autonomously initiate new transactions on the account’s behalf.

Hooks can be written in C or any other preferred language and then compiled into WebAssembly.

<figure><img src="https://cdn.feather.blog/?src=https%3A%2F%2Fusenotioncms.com%2Fproxy%2Fblock%2Fd315cbec-a4e7-4345-ba48-07d936239181%252F02a28a46-80d0-4e64-a96d-33497950a60f%252Fimage_(7).png&#x26;optimizer=image" alt="Using Hooks Builder, you can develop, test, debug and deploy your own Hooks on our testnet, using our examples or building your own from scratch." height="100%"><figcaption></figcaption></figure>

The Hooks Builder serves as an integrated development environment, facilitating the crafting, testing, debugging, and deployment of your Hooks on our testnet.

Whether you're utilizing our examples or building from scratch, Hooks Builder provides a helpful environment for honing and deploying your smart contract solutions.

### Some Examples of specific Hooks and Use Cases <a href="#some-examples-of-specific-hooks" id="some-examples-of-specific-hooks"></a>

Showcasing the potential of Hooks with these concrete examples, each illustrating a unique application of smart contract functionality on the XRPL:

* **Auto-Savings Hook**: Automate savings by configuring a Hook to transfer a set amount of XRP to a separate savings account on the ledger. This could be done to help save a portion of XRP and build up savings at specified intervals—daily, weekly, or monthly. This recurring transfer mechanism can be a base for developing personal finance applications or subscription-based models.
* **Carbon-Offset Hook**: Each transaction triggers an additional transfer of 1% of the amount to a carbon offset account managed by a trusted non-governmental organization (NGO) using the money for a good cause. This feature can be used as a base for building applications that contribute to environmental sustainability with every transaction made.
* **Firewall Hook**: By filtering incoming and outgoing transactions. The Firewall Hook can block malicious transactions originating from known scam accounts or containing suspicious memos. By retrieving an updated blocklist from a Hook on a different account, the firewall maintains a robust defense against fraud without the need for manual intervention. Additionally, implementing spending limits to deny high-value unauthorized withdrawals could be a crucial feature for financial applications.

## **Distinguishing Hooks from Ethereum Virtual Machine (EVM)**

XRPL Hooks and the EVM allow developers to build and deploy custom logic and automation within their platforms. However, some key differences between these two technologies set them apart.&#x20;

* **Platform Compatibility**: Hooks are tailored for the XRP Ledger, while EVM smart contracts are designed for Ethereum-based blockchains.
* **Execution Efficiency**: Hooks utilize WebAssembly (WASM), outperforming the bytecode used by the EVM in terms of speed and efficiency.
* **Predictable Execution Time**: XRPL Hooks use guards to ensure maximum execution time is well-bounded and known ahead of time, improving efficiency.

### Alternatives to Hooks on the XRPL <a href="#alternatives-to-hooks-on-the-xrpl" id="alternatives-to-hooks-on-the-xrpl"></a>

Ripple and Peersyst announced that an EVM-compatible sidechain is now live [on the company’s devnet](https://xrpl.org/evm-sidechains.html). A sidechain is an independent ledger with its own consensus algorithm and transaction types and rules. It acts as its own blockchain.The EVM sidechain is an alternative to Hooks that adds a type of smart contract functionality to the ecosystem.However, sidechains operate on Layer 2, so any smart contracts running on the sidechain are not directly integrated into the XRPL.In order to use the smart contract functionality of the sidechain, XRP first has to be swapped onto the sidechain, then later swapped back. This means the transaction essentially gets processed twice. Once on the sidechain, then again on the XRPL, meaning Layer 2 smart contracts cannot influence the flow.Hooks can decide if a transaction is allowed in the first place. Layer 2 can make a retroactive decision, but the initial transaction has already happened.Hooks are more closely integrated with XRPL, operating directly on Layer 1 of the XRPL, so they are more tightly integrated with the underlying blockchain technology than the EVM-Compatible Sidechain to take advantage of the specific features and capabilities of the XRPL platform.Hooks are implemented using WebAssembly, designed for high-performance environments such as edge computing.

### Hooks will expand the on-ledger functionality and help XRPL grow <a href="#hooks-will-expand-the-on-ledger-functionality-and-help-xrpl-grow" id="hooks-will-expand-the-on-ledger-functionality-and-help-xrpl-grow"></a>

Hooks will bring native smart contract functionality to the XRPL, allowing the development of custom applications tailored to the specific needs and requirements of the account holder, opening up whole new domains of functionality, as the possibilities with Hooks are almost unlimited.As the XRPL continues to grow, there is no doubt that Hooks will play a significant role in driving further innovation and adoption of the platform by retail and enterprise users.
