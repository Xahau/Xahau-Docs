# Payments

The Payments feature in the Xahau network is a crucial component that enables the transfer of assets and funds within the network. This feature is designed to facilitate seamless transactions, ensuring a smooth and efficient operation of the network.

### Transaction Types

The Payments feature comprises several transaction types, each serving a unique purpose in the network. Here's a brief overview of each transaction type:

**DepositPreauth**

This transaction type allows an account to preauthorize incoming transactions from a specified source. It's a way to whitelist accounts, ensuring that only authorized transactions are processed.

{% content-ref url="../../technical/protocol-reference/transactions/transaction-types/depositpreauth.md" %}
[depositpreauth.md](../../technical/protocol-reference/transactions/transaction-types/depositpreauth.md)
{% endcontent-ref %}

**TrustSet**

This transaction type allows users to create a trust line with another account. It's a way to establish trust between two accounts, enabling them to transact with each other.

{% content-ref url="../../technical/protocol-reference/transactions/transaction-types/trustset.md" %}
[trustset.md](../../technical/protocol-reference/transactions/transaction-types/trustset.md)
{% endcontent-ref %}

**Payment**

This is the basic transaction type that allows the transfer of assets between accounts. It's the fundamental transaction type for any payment operation in the network.

{% content-ref url="../../technical/protocol-reference/transactions/transaction-types/payment.md" %}
[payment.md](../../technical/protocol-reference/transactions/transaction-types/payment.md)
{% endcontent-ref %}

**PaymentChannelCreate**

This transaction type allows the creation of a payment channel between two accounts. Payment channels are off-ledger scalability solutions that enable high-frequency, low-cost transactions between two parties.

{% content-ref url="../../technical/protocol-reference/transactions/transaction-types/paymentchannelcreate.md" %}
[paymentchannelcreate.md](../../technical/protocol-reference/transactions/transaction-types/paymentchannelcreate.md)
{% endcontent-ref %}

**PaymentChannelFund**

This transaction type allows an account to fund an existing payment channel. It's a way to add more assets to a payment channel, enabling more transactions to take place.

{% content-ref url="../../technical/protocol-reference/transactions/transaction-types/paymentchannelfund.md" %}
[paymentchannelfund.md](../../technical/protocol-reference/transactions/transaction-types/paymentchannelfund.md)
{% endcontent-ref %}

**PaymentChannelClaim**

This transaction type allows an account to claim the funds from a payment channel. It's a way to close a payment channel and retrieve the remaining assets.

{% content-ref url="../../technical/protocol-reference/transactions/transaction-types/paymentchannelclaim.md" %}
[paymentchannelclaim.md](../../technical/protocol-reference/transactions/transaction-types/paymentchannelclaim.md)
{% endcontent-ref %}
