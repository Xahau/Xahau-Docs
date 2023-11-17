# URIToken

URITokens are the Non-Fungible Token (NFT) implementation native to the Xahau network. They exist as first-class on-ledger objects, uniquely identified by the hash of their issuer and Uniform Resource Identifier (URI). URITokens can point to any digital content, with only one object per URI per account existing on the ledger.

The issuer has the ability to set a flag to enable the burning of the object in the future. Each owner's reserve is locked up as well upon ownership of the URIToken.

### Transaction Types

#### URITokenMint

The URITokenMint transaction mints a new URIToken and assigns ownership to the specified account. The minted URIToken represents a unique digital asset that can be used in various applications. The issuer can choose to allow the minted URIToken to be destroyed in the future.

{% content-ref url="../../technical/protocol-reference/transactions/transaction-types/uritokenmint.md" %}
[uritokenmint.md](../../technical/protocol-reference/transactions/transaction-types/uritokenmint.md)
{% endcontent-ref %}

#### URITokenBurn

The URITokenBurn transaction is used to burn a URIToken in Xahau. Burning a URIToken permanently removes it from circulation. The transaction does not have any special transaction cost requirements. The account that owns the URIToken to be burned is required for this transaction.

{% content-ref url="../../technical/protocol-reference/transactions/transaction-types/uritokenburn.md" %}
[uritokenburn.md](../../technical/protocol-reference/transactions/transaction-types/uritokenburn.md)
{% endcontent-ref %}

#### URITokenBuy

The URITokenBuy transaction allows a user to buy a URIToken from the issuer. This transaction is used to transfer ownership of a URIToken from the issuer to the buyer. The buyer's account, the unique identifier of the URIToken to be bought, and the amount of currency to pay for the URIToken are required for this transaction.

{% content-ref url="../../technical/protocol-reference/transactions/transaction-types/uritokenbuy.md" %}
[uritokenbuy.md](../../technical/protocol-reference/transactions/transaction-types/uritokenbuy.md)
{% endcontent-ref %}

{% content-ref url="../../technical/protocol-reference/transactions/transaction-types/uritokencreateselloffer.md" %}
[uritokencreateselloffer.md](../../technical/protocol-reference/transactions/transaction-types/uritokencreateselloffer.md)
{% endcontent-ref %}

{% content-ref url="../../technical/protocol-reference/transactions/transaction-types/uritokencancelselloffer.md" %}
[uritokencancelselloffer.md](../../technical/protocol-reference/transactions/transaction-types/uritokencancelselloffer.md)
{% endcontent-ref %}
