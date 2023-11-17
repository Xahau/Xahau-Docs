# Hooks

Hooks are a powerful feature of the XRPL network, providing robust smart contract functionality. They are small, efficient WebAssembly modules designed specifically for the XRPL, and can be referred to as Smart Contracts for the XRP Ledger Protocol. Hooks can be written in any language that is compilable with WebAssembly, allowing for a wide range of business logic and smart contract concepts to be implemented.

### Transaction Types

The Hooks feature includes two types of transactions:

**SetHook**

This transaction type is used to set up a hook on an account.

{% content-ref url="../../technical/protocol-reference/transactions/transaction-types/sethook.md" %}
[sethook.md](../../technical/protocol-reference/transactions/transaction-types/sethook.md)
{% endcontent-ref %}

**Invoke**

This transaction type is used to call or invoke the functionality of a hook.

{% content-ref url="../../technical/protocol-reference/transactions/transaction-types/invoke.md" %}
[invoke.md](../../technical/protocol-reference/transactions/transaction-types/invoke.md)
{% endcontent-ref %}
