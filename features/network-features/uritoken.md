---
description: >-
  URITokens are the Non-Fungible Token (NFT) implementation native to the
  network. Every NFT is a native ledger object.
---

# URIToken

URITokens are Non-Fungible Tokens (NFTs) that exist as first-class on-ledger objects.

They are uniquely identified by the hash of their issuer and Uniform Resource Identifier (URI), and can point to any digital content.

Only one object per URI per account can exist on the ledger.

The Issuer can set a flag to enable burning of the object in the future. Each owner's reserve is locked up as well upon ownership of the URIToken.

They include the transaction types; `mint`, `burn`, `buy`, `create sell offer`, and `cancel sell offer`. Additionally, when minting a URIToken, users can choose whether or not to include a SHA-512 Half hash of the URI's contents to ensure data integrity.

### Transaction Types

{% content-ref url="../transaction-types/uritokenmint.md" %}
[uritokenmint.md](../transaction-types/uritokenmint.md)
{% endcontent-ref %}

{% content-ref url="../transaction-types/uritokenburn.md" %}
[uritokenburn.md](../transaction-types/uritokenburn.md)
{% endcontent-ref %}

{% content-ref url="../transaction-types/uritokencreateselloffer.md" %}
[uritokencreateselloffer.md](../transaction-types/uritokencreateselloffer.md)
{% endcontent-ref %}

{% content-ref url="../transaction-types/uritokencancelselloffer.md" %}
[uritokencancelselloffer.md](../transaction-types/uritokencancelselloffer.md)
{% endcontent-ref %}

{% content-ref url="../transaction-types/uritokenbuy.md" %}
[uritokenbuy.md](../transaction-types/uritokenbuy.md)
{% endcontent-ref %}
