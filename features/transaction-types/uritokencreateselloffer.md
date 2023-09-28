---
description: >-
  An URITokenCreateSellOffer transaction allows a user to create a sell offer
  for a URIToken on the XRP Ledger's decentralized exchange.
---

# URITokenCreateSellOffer

\[[Source](https://github.com/Xahau/xahaud/blob/dev/src/ripple/app/tx/impl/URIToken.cpp)]

_(Added by the \[URIToken amendment]\[].)_

### Example

```json
{
    "TransactionType": "URITokenCreateSellOffer",
    "Account": "rPT1Sjq2YGrBMTttX4GZHjKu9dyfzbpAYe",
    "URITokenID": "C1AE6DDDEEC05CF2978C0BAD6FE27362498DGS691DC749DCDD3B95992978C0BA",
    "Destination": "rPT1Sjq2YGrBMTttX4GZHjKu9dyfzbpAYe",
    "Amount": {
      "issuer": "rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn",
      "currency": "USD",
      "value": "100",
    },
}
```

{% hint style="info" %}
[Query Example Tx](http://localhost:4000/tx?binary=false\&id=example\_URITokenBurn\&transaction=C53ECF838647FA5A4C780377025FEC7999AB4182590510CA461444B207AB74A9)
{% endhint %}

### Fields

<table><thead><tr><th width="172">Field</th><th width="137">JSON Type</th><th>[Internal Type][]</th><th>Description</th></tr></thead><tbody><tr><td><code>Account</code></td><td>String</td><td>AccountID</td><td>The address of the account creating the sell offer.</td></tr><tr><td><code>URITokenID</code></td><td>String</td><td>Hash256</td><td>The ID of the URIToken being sold.</td></tr><tr><td><code>Destination</code></td><td>String</td><td>AccountID</td><td><em>(Optional)</em> The address of the account to receive the sell offer.</td></tr><tr><td><code>Amount</code></td><td>[Currency Amount][]</td><td>Amount</td><td>The amount of currency the account wants to receive in exchange for the URIToken.</td></tr></tbody></table>

### Error Cases

Besides errors that can occur for all transactions, URITokenCreateSellOffer transactions can result in the following transaction result codes:

| Error Code               | Description                                                                      |
| ------------------------ | -------------------------------------------------------------------------------- |
| `tecNO_TARGET`           | Occurs if the target account does not exist.                                     |
| `tecNO_PERMISSION`       | Occurs if the account does not have permission to create a sell offer.           |
| `tecINSUF_RESERVE_LINE`  | Occurs if the account does not have a sufficient reserve to create a sell offer. |
| `tecINSUF_RESERVE_OFFER` | Occurs if the account does not have a sufficient reserve to create a sell offer. |
| `tecUNFUNDED_OFFER`      | Occurs if the account does not have a sufficient balance to create a sell offer. |
| `tecOFFER_INVALID`       | Occurs if the sell offer is invalid.                                             |
