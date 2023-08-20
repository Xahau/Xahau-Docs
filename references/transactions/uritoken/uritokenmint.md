---
html: uritokenmint.html
title: Mint a URIToken.
tags:
  - URIToken
---

# URITokenMint

[[Source]](https://github.com/ripple/rippled/blob/develop/src/ripple/app/tx/impl/URIToken.cpp "Source")

_(Added by the [URIToken amendment][].)_

An URIToken Mint transaction mints a new URIToken and assigns ownership to the specified account. The URIToken represents a unique digital asset that can be used in various applications. This transaction is used to create new URITokens and add them to the owner's inventory.

## Example URITokenMint JSON

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

[Query example transaction. >](websocket-api-tool.html?server=wss%3A%2F%2Fxrplcluster.com%2F&req=%7B%22id%22%3A%22example_URITokenMint%22%2C%22command%22%3A%22tx%22%2C%22transaction%22%3A%221AF19BF9717DA0B05A3BFC5007873E7743BA54C0311CCCCC60776AAEAC5C4635%22%2C%22binary%22%3Afalse%7D)

| Field           | JSON Type            | [Internal Type][]    | Description                  |
|:----------------|:---------------------|:---------------------|:-----------------------------|
| `Account`       | String               | AccountID            | The address of the account that will own the minted URIToken. |
| `URI`           | String               | String               | The URI associated with the minted URIToken. |
| `Digest`        | String               | Hash256              | _(Optional)_ The digest of the URIToken. |
| `Destination`   | String               | AccountID            | _(Optional)_ The address of the account that can buy the minted URIToken. |
| `Amount`        | [Currency Amount][]  | Amount               | _(Optional)_ The amount of currency the account wants to receive in exchange for the URIToken. |

## Special Transaction Cost

The URIToken Mint transaction has a standard transaction cost, which is the minimum transaction cost required for all transactions.

## Error Cases

Besides errors that can occur for all transactions, URIToken Mint transactions can result in the following transaction result codes:

| Error Code | Description |
|:-----------|:------------|
| `tecDUPLICATE` | Occurs if a URIToken with the same URI already exists. |
| `tecDIR_FULL` | Occurs if the owner's directory is full and cannot accommodate the new URIToken. |
| `terNO_ACCOUNT` | Occurs if the sending account does not exist. |
