# Escrow

The Escrow feature is a crucial part of the Xahau network. It provides a secure and trustless method for transactions between parties. The Escrow feature ensures that the assets involved in a transaction are held securely until all the conditions of the transaction are met.

### Transaction Types

The Escrow feature includes three types of transactions:

#### EscrowCreate

The `EscrowCreate` transaction is used to create a new escrow agreement. This transaction specifies the terms of the escrow, including the parties involved, the assets to be held in escrow, and the conditions under which the assets will be released.

{% content-ref url="../../technical/protocol-reference/transactions/transaction-types/escrowcreate.md" %}
[escrowcreate.md](../../technical/protocol-reference/transactions/transaction-types/escrowcreate.md)
{% endcontent-ref %}

#### EscrowFinish

The `EscrowFinish` transaction is used to complete an escrow agreement. This transaction is executed when all the conditions of the escrow are met. Upon execution, the assets held in escrow are released to the appropriate party.

{% content-ref url="../../technical/protocol-reference/transactions/transaction-types/escrowfinish.md" %}
[escrowfinish.md](../../technical/protocol-reference/transactions/transaction-types/escrowfinish.md)
{% endcontent-ref %}

#### EscrowCancel

The `EscrowCancel` transaction is used to cancel an escrow agreement. This transaction can be executed if the conditions of the escrow are not met within a specified time frame. Upon cancellation, the assets held in escrow are returned to the party that initiated the escrow.

{% content-ref url="../../technical/protocol-reference/transactions/transaction-types/escrowcancel.md" %}
[escrowcancel.md](../../technical/protocol-reference/transactions/transaction-types/escrowcancel.md)
{% endcontent-ref %}
