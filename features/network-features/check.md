# Check

The Check feature in the Xahau network is a deferred payment system that allows for the creation, cancellation, and cashing of checks within the ledger. This feature is designed to facilitate secure and efficient transactions between parties.

### Transaction Types

#### CheckCreate

The `CheckCreate` transaction is used to create a Check object in the ledger. This represents a deferred payment that can be cashed by its intended destination.&#x20;

{% content-ref url="../../technical/protocol-reference/transactions/transaction-types/checkcreate.md" %}
[checkcreate.md](../../technical/protocol-reference/transactions/transaction-types/checkcreate.md)
{% endcontent-ref %}

#### CheckCancel

The `CheckCancel` transaction is used to cancel a Check that has been created but not yet cashed. This allows the sender to stop the payment from being processed if necessary.

{% content-ref url="../../technical/protocol-reference/transactions/transaction-types/checkcancel.md" %}
[checkcancel.md](../../technical/protocol-reference/transactions/transaction-types/checkcancel.md)
{% endcontent-ref %}

#### CheckCash

The `CheckCash` transaction is used to cash a Check that has been created. This allows the recipient to receive the funds that have been deferred.

{% content-ref url="../../technical/protocol-reference/transactions/transaction-types/checkcash.md" %}
[checkcash.md](../../technical/protocol-reference/transactions/transaction-types/checkcash.md)
{% endcontent-ref %}
