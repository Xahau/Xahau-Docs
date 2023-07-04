---
description: 'Hooks: bringing (composability) Smart Contracts to the XRP Ledger Protocol'
cover: .gitbook/assets/cdn.feather.webp
coverY: 0
---

# Hooks

{% hint style="info" %}
Hooks are small, efficient WebAssembly modules designed specifically for the XRPL. They could be referred to as **Smart Contracts for the XRP Ledger Protocol**.

Hooks can be written in any language (compilable to WebAssembly) and most business logic and most smart contract concepts can be implemented in a hook.

[**Development by XRPL Labs**](https://xrpl-labs.com/#team)
{% endhint %}

### What are Hooks? <a href="#what-are-hooks" id="what-are-hooks"></a>

Hooks allow the creation of customized logic and automation within the XRPL, making transactions smarter and more convenient.These small, efficient modules add custom on-ledger functionality, such as creating custom triggers for specific events on the ledger. These triggers can be used to send on-ledger actions or execute other actions in response to the specified event.Hooks are currently only available on the [XRPL Labs public Hooks testnet,](https://hooks-testnet-v2.xrpl-labs.com/) as the feature is under development.&#x20;

> _There is a_ [_Hooks Builder site_](https://hooks.xrpl.org/) _where you can develop, test, debug, and deploy your own Hooks on testnet in your browser, using our examples or building your own from scratch._

### Why are Hooks a big deal? <a href="#why-are-hooks-a-big-deal" id="why-are-hooks-a-big-deal"></a>

&#x20;Simply put, Hooks add smart contract functionality to the XRPL. They give you the freedom to build and deploy your applications with functionality tailored to your specific needs and requirements. They can be used to implement most business logic and smart contract ideas.Once a hook is set up on an account, it can allow you to:

* Block or allow transactions to and from the account.
* Change and keep track of the hook’s internal state and logic to inform programmatic choices.
* Send out new transactions on the account’s behalf.

Hooks can be written in C or any other language and then compiled into WebAssembly.

<figure><img src="https://cdn.feather.blog/?src=https%3A%2F%2Fusenotioncms.com%2Fproxy%2Fblock%2Fd315cbec-a4e7-4345-ba48-07d936239181%252F02a28a46-80d0-4e64-a96d-33497950a60f%252Fimage_(7).png&#x26;optimizer=image" alt="Using Hooks Builder, you can develop, test, debug and deploy your own Hooks on our testnet, using our examples or building your own from scratch." height="100%"><figcaption></figcaption></figure>

Using Hooks Builder, you can develop, test, debug and deploy your own Hooks on our testnet, using our examples or building your own from scratch.

### Some examples of specific Hooks <a href="#some-examples-of-specific-hooks" id="some-examples-of-specific-hooks"></a>

&#x20;Auto-Savings Hook Automatically transfer a set amount of XRP into a separate savings account on the ledger. This could be done regularly, such as daily, weekly, or monthly, to help the person save a portion of their XRP and build up their savings.Carbon-Offset Hook When sending funds, an extra transaction is sent out for 1% of the amount spent. This transaction is sent to a carbon offset account run by a non-governmental organization (NGO), which will use the money to plant trees.Firewall Hook Malicious small transactions containing memos or outgoing payments to confirmed scam accounts are blocked. The hook can retrieve a blocklist from a different hook installed on a different account. This means the user does not need to update their firewall to remain safe. Additionally, the user can impose spending limits to prevent high amounts from being withdrawn.

### How do Hooks differ from an Ethereum Virtual Machine (EVM)? <a href="#how-do-hooks-differ-from-an-ethereum-virtual-machine-evm" id="how-do-hooks-differ-from-an-ethereum-virtual-machine-evm"></a>

XRPL Hooks and the EVM both allow developers to build and deploy custom logic and automation within their respective platforms. However, some key differences between these two technologies set them apart.One of the main differences between Hooks and EVM is the platform they are designed to work with. Hooks are specifically designed to work within the XRP Ledger, while EVM smart contracts only work with Ethereum-based blockchains.Hooks are more efficient because they use WebAssembly (WASM), which is faster and more efficient than the bytecode used by the Ethereum Virtual Machine.Additionally, XRPL Hooks use guards to ensure that maximum execution time is well-bounded and known ahead of time, which helps to improve efficiency.

### Alternatives to Hooks on the XRPL <a href="#alternatives-to-hooks-on-the-xrpl" id="alternatives-to-hooks-on-the-xrpl"></a>

Ripple and Peersyst announced that an EVM-compatible sidechain is now live [on the company’s devnet](https://xrpl.org/evm-sidechains.html). A sidechain is an independent ledger with its own consensus algorithm and transaction types and rules. It acts as its own blockchain.The EVM sidechain is an alternative to Hooks that adds a type of smart contract functionality to the ecosystem.However, sidechains operate on Layer 2, so any smart contracts running on the sidechain are not directly integrated into the XRPL.In order to use the smart contract functionality of the sidechain, XRP first has to be swapped onto the sidechain, then later swapped back. This means the transaction essentially gets processed twice. Once on the sidechain, then again on the XRPL, meaning Layer 2 smart contracts cannot influence the flow.Hooks can decide if a transaction is allowed in the first place. Layer 2 can make a retroactive decision, but the initial transaction has already happened.Hooks are more closely integrated with XRPL, operating directly on Layer 1 of the XRPL, so they are more tightly integrated with the underlying blockchain technology than the EVM-Compatible Sidechain to take advantage of the specific features and capabilities of the XRPL platform.Hooks are implemented using WebAssembly, designed for high-performance environments such as edge computing.

### Hooks will expand the on-ledger functionality and help XRPL grow <a href="#hooks-will-expand-the-on-ledger-functionality-and-help-xrpl-grow" id="hooks-will-expand-the-on-ledger-functionality-and-help-xrpl-grow"></a>

Hooks will bring native smart contract functionality to the XRPL, allowing the development of custom applications tailored to the specific needs and requirements of the account holder, opening up whole new domains of functionality, as the possibilities with Hooks are almost unlimited.As the XRPL continues to grow, there is no doubt that Hooks will play a significant role in driving further innovation and adoption of the platform by retail and enterprise users.
