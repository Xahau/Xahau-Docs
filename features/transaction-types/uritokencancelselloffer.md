---
description: >-
  An URITokenCancelSellOffer transaction cancels a sell offer for a URIToken in
  the XRP Ledger.
---

# URITokenCancelSellOffer

\[[Source](https://github.com/Xahau/xahaud/blob/dev/src/ripple/app/tx/impl/URIToken.cpp)]

_(Added by the \[URIToken amendment]\[].)_

### Example

```json
{
    "TransactionType": "URITokenCancelSellOffer",
    "Account": "r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59",
    "URITokenID": "C1AE6DDDEEC05CF2978C0BAD6FE27362498DGS691DC749DCDD3B95992978C0BA",
}
```



{% hint style="info" %}
[Query Example Tx](http://localhost:4000/tx?binary=false\&id=example\_URITokenBurn\&transaction=C53ECF838647FA5A4C780377025FEC7999AB4182590510CA461444B207AB74A9)
{% endhint %}

### Fields

<table><thead><tr><th width="166">Field</th><th width="114">JSON Type</th><th width="177">[Internal Type][]</th><th>Description</th></tr></thead><tbody><tr><td><code>Account</code></td><td>String</td><td>AccountID</td><td>The address of the account that owns the sell offer to cancel.</td></tr><tr><td><code>URITokenID</code></td><td>String</td><td>Hash256</td><td>The ID of the URIToken to cancel the sell offer.</td></tr></tbody></table>

### Error Cases

Besides errors that can occur for all transactions, \{{currentpage.name\}} transactions can result in the following transaction result codes:

| Error Code    | Description                                        |
| ------------- | -------------------------------------------------- |
| `tecNO_ENTRY` | Occurs if the specified sell offer does not exist. |
