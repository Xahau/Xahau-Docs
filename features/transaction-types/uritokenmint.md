---
description: >-
  An URIToken Mint transaction mints a new URIToken and assigns ownership to the
  specified account. The URIToken represents a unique digital asset that can be
  used in various applications.
---

# URITokenMint

\[[Source](https://github.com/Xahau/xahaud/blob/dev/src/ripple/app/tx/impl/URIToken.cpp)]

_(Added by the \[URIToken amendment]\[].)_

### Example

```json
{
    "TransactionType": "URITokenMint",
    "Account": "rWYkbWkCeg8dP6rXALnjgZSjjLyih5NXm",
    "Flags": 1,
    "URI": "697066733A2F2F4445414442454546",
    "Digest": "697066733A2F2F4445414442454546697066733A2F2F44454144424545467878",
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

<table><thead><tr><th width="173">Field</th><th width="150">JSON Type</th><th>[Internal Type][]</th><th>Description</th></tr></thead><tbody><tr><td><code>Account</code></td><td>String</td><td>AccountID</td><td>The address of the account that will own the minted URIToken.</td></tr><tr><td><code>URI</code></td><td>String</td><td>String</td><td>The URI associated with the minted URIToken.</td></tr><tr><td><code>Digest</code></td><td>String</td><td>Hash256</td><td><em>(Optional)</em> The digest of the URIToken.</td></tr><tr><td><code>Destination</code></td><td>String</td><td>AccountID</td><td><em>(Optional)</em> The address of the account that can buy the minted URIToken.</td></tr><tr><td><code>Amount</code></td><td>[Currency Amount][]</td><td>Amount</td><td><em>(Optional)</em> The amount of currency the account wants to receive in exchange for the URIToken.</td></tr></tbody></table>

### Special Transaction Cost

The URIToken Mint transaction has a standard transaction cost, which is the minimum transaction cost required for all transactions.

### Error Cases

Besides errors that can occur for all transactions, URIToken Mint transactions can result in the following transaction result codes:

| Error Code      | Description                                                                      |
| --------------- | -------------------------------------------------------------------------------- |
| `tecDUPLICATE`  | Occurs if a URIToken with the same URI already exists.                           |
| `tecDIR_FULL`   | Occurs if the owner's directory is full and cannot accommodate the new URIToken. |
| `terNO_ACCOUNT` | Occurs if the sending account does not exist.                                    |
