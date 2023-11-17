# Account Managment

The Account Management features in the Xahau network is a crucial component that allows users to manage their accounts effectively. This feature includes several transaction types that enable users to perform various operations on their accounts.

### Transaction Types

#### AccountSet

The `AccountSet` transaction type allows users to modify the properties of their accounts. This includes settings such as transfer rate, account flags, and more.

{% content-ref url="../../technical/protocol-reference/transactions/transaction-types/accountset.md" %}
[accountset.md](../../technical/protocol-reference/transactions/transaction-types/accountset.md)
{% endcontent-ref %}

#### AccountDelete

The `AccountDelete` transaction type enables users to delete their accounts from the Xahau network. This operation is irreversible and should be used with caution.

{% content-ref url="../../technical/protocol-reference/transactions/transaction-types/accountdelete.md" %}
[accountdelete.md](../../technical/protocol-reference/transactions/transaction-types/accountdelete.md)
{% endcontent-ref %}

#### SetRegularKey

The `SetRegularKey` transaction type allows users to set a regular key pair for their account. This key pair can be used as an alternative to the master key pair for signing transactions.

{% content-ref url="../../technical/protocol-reference/transactions/transaction-types/setregularkey.md" %}
[setregularkey.md](../../technical/protocol-reference/transactions/transaction-types/setregularkey.md)
{% endcontent-ref %}

#### SignersListSet

The `SignersListSet` transaction type enables users to set a list of signers for their account. This is particularly useful for multi-signature accounts where multiple parties are required to sign off on transactions.

{% content-ref url="../../technical/protocol-reference/transactions/transaction-types/signerlistset.md" %}
[signerlistset.md](../../technical/protocol-reference/transactions/transaction-types/signerlistset.md)
{% endcontent-ref %}

#### Import

The `Import` transaction type is used to import transactions from other networks. This feature is especially useful for issuers who need to import transactions for their asset holders. It's recommended to key your accounts first before attempting to import transactions.

Please note that the process of importing for the issuer involves specific transaction types and requires careful configuration. Always ensure that the hooks are correctly set up and that the transactions are valid for the intended operations.

These transaction types provide users with a comprehensive set of tools for managing their accounts on the Xahau network. As with all operations, users should ensure they understand the implications of each transaction type before use.

{% content-ref url="../../technical/protocol-reference/transactions/transaction-types/import.md" %}
[import.md](../../technical/protocol-reference/transactions/transaction-types/import.md)
{% endcontent-ref %}
