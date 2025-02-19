---
description: 'Introducing Hooks: The Smart Contract Functionality for Xahau.'
cover: .gitbook/assets/cdn.feather.webp
coverY: 0
---

# 🪝 Hooks



{% hint style="info" %}
Hooks are small, efficient WebAssembly modules designed specifically for Xahau.&#x20;

Hooks can be written in any language (compilable with WebAssembly), and most business logic and smart contract concepts can be implemented in a hook.

[**Development by XRPL Labs**](https://xrpl-labs.com/#team)
{% endhint %}

### What are Hooks? <a href="#what-are-hooks" id="what-are-hooks"></a>

Hooks allow the creation of customized logic and automation within the Xahau, making transactions smarter and more convenient. These small, efficient modules add custom on-ledger functionality, such as creating custom triggers for specific events on the ledger.&#x20;

These triggers can be used to send on-ledger actions or execute other actions in response to the specified event. Hooks are currently available on the [Xahau network](https://xahau.network/).

> _To learn more about the theoretical concepts of Hooks you can visit the_ [_Concepts_](concepts/) _section._

> _To learn how to code Hooks in C and its functions, visit_ [_Hooks C-Functions_](technical/hooks-functions/)_._

> _There is a_ [_Hooks Builder site_](https://builder.xahau.network/) _where you can develop, test, debug, and deploy your own Hooks on testnet in your browser, using our examples or building your own from scratch._

> There is an upcoming development to allow writing Hooks in Javascript, also known as JSHooks. At the moment it can be tested using [JSHooks](https://github.com/Xahau/jshooks-alpha) repo.

### Why are Hooks a Big Deal? <a href="#why-are-hooks-a-big-deal" id="why-are-hooks-a-big-deal"></a>

Simply put, Hooks add a robust smart contract functionality to Xahau, empowering you to construct and deploy applications with bespoke functionalities aligning with your specific needs and requirements.

Hooks provide a versatile platform as they can be used for implementing a broad spectrum of business logic and smart contract paradigms. Once a hook is set up on an account, it enables you to do the following:

* Block or allow transactions to and from the account.
* Change and keep track of the hook’s internal state and logic to inform programmatic choices.
* Autonomously initiate new transactions on the account’s behalf.

Hooks can be written in C or any other preferred language and then compiled into WebAssembly.

<figure><img src="https://cdn.feather.blog/?src=https%3A%2F%2Fusenotioncms.com%2Fproxy%2Fblock%2Fd315cbec-a4e7-4345-ba48-07d936239181%252F02a28a46-80d0-4e64-a96d-33497950a60f%252Fimage_(7).png&#x26;optimizer=image" alt="Using Hooks Builder, you can develop, test, debug and deploy your own Hooks on our testnet, using our examples or building your own from scratch." height="100%"><figcaption></figcaption></figure>

The Hooks Builder serves as an integrated development environment, facilitating the crafting, testing, debugging, and deployment of your Hooks on our testnet.

Whether you're utilizing our examples or building from scratch, Hooks Builder provides a helpful environment for honing and deploying your smart contract solutions.

### Some Examples of specific Hooks and Use Cases <a href="#some-examples-of-specific-hooks" id="some-examples-of-specific-hooks"></a>

Showcasing the potential of Hooks with these concrete examples, each illustrating a unique application of smart contract functionality on Xahau:

* **Auto-Savings Hook**: Automate savings by configuring a Hook to transfer a set amount of XAH to a separate savings account on the ledger. This could be done to help save a portion of XAH and build up savings at specified intervals—daily, weekly, or monthly. This recurring transfer mechanism can be a base for developing personal finance applications or subscription-based models.
* **Carbon-Offset Hook**: Each transaction triggers an additional transfer of 1% of the amount to a carbon offset account managed by a trusted non-governmental organization (NGO) using the money for a good cause. This feature can be used as a base for building applications that contribute to environmental sustainability with every transaction made.
* **Firewall Hook**: By filtering incoming and outgoing transactions. The Firewall Hook can block malicious transactions originating from known scam accounts or containing suspicious memos. By retrieving an updated blocklist from a Hook on a different account, the firewall maintains a robust defense against fraud without the need for manual intervention. Additionally, implementing spending limits to deny high-value unauthorized withdrawals could be a crucial feature for financial applications.

### **Distinguishing Hooks from Ethereum Virtual Machine (EVM)**

Xahau Hooks and the EVM allow developers to build and deploy custom logic and automation within their platforms. However, some key differences between these two technologies set them apart.&#x20;

* **Platform Compatibility**: Hooks are tailored for Xahau, while EVM smart contracts are designed for Ethereum-based blockchains.
* **Execution Efficiency**: Hooks utilize WebAssembly (WASM), outperforming the bytecode used by the EVM in terms of speed and efficiency.
* **Predictable Execution Time**: Xahau Hooks use guards to ensure maximum execution time is well-bounded and known ahead of time, improving efficiency.

### Alternatives to Hooks on the XRPL ecosystem

Ripple and Peersyst announced that an EVM-compatible sidechain is now live [on the company's devnet](https://opensource.ripple.com/docs/evm-sidechain/intro-to-evm-sidechain/). This sidechain functions as an autonomous blockchain, complete with its unique consensus protocol and transaction rules. The EVM sidechain is an alternative to Hooks, adding smart contract functionality to the ecosystem.&#x20;

However, it's essential to note that EVM sidechain contracts function on Layer 2, which requires a two-step process where XRP is transitioned onto the sidechain for contract execution and then back to the main ledger. Once on the sidechain, then again on the XRPL, meaning Layer 2 smart contracts cannot influence the flow. Hooks can decide if a transaction is allowed in the first place. Layer 2 can make a retroactive decision, but the initial transaction has already happened.

Hooks are more closely integrated with XRPL, operating directly on Xahau, an Layer 1 XRPL-core fork, so they are more tightly integrated with the underlying blockchain technology than the EVM-compatible sidechain to take advantage of the specific features and capabilities of the XRPL platform. With the inherent scalability and performance of WebAssembly, Hooks are optimal to enhance Xahau's functionality.

### Hooks Will Expand the On-ledger Functionality and Help Xahau Grow

Hooks add native smart contract capabilities to Xahau, enabling the crafting of custom applications that meet the unique needs of users, bringing new functionalities, and opening up whole new domains of functionality. With Hooks, the possibilities are virtually unlimited.

As Xahau continues to grow, there is no doubt that Hooks will play a significant role in driving further innovation and adoption of the platform by retail and enterprise users.
