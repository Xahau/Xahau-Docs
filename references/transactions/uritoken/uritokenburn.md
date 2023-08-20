---
html: uritokenburn.html
title: Burn a URIToken.
tags:
  - URIToken
---
# URITokenBurn

[[Source]](https://github.com/ripple/rippled/blob/develop/src/ripple/app/tx/impl/URIToken.cpp "Source")

_(Added by the [URIToken amendment][].)_

The URITokenBurn transaction is used to burn a URIToken in the XRP Ledger. Burning a URIToken permanently removes it from circulation.

## Example URITokenBurn JSON

```json
{
    "TransactionType": "URITokenBurn",
    "Account": "rWYkbWkCeg8dP6rXALnjgZSjjLyih5NXm",
    "URITokenID": "C1AE6DDDEEC05CF2978C0BAD6FE27362498DGS691DC749DCDD3B95992978C0BA",
}
```

[Query example transaction. >](websocket-api-tool.html?server=wss%3A%2F%2Fxrplcluster.com%2F&req=%7B%22id%22%3A%22example_URITokenBurn%22%2C%22command%22%3A%22tx%22%2C%22transaction%22%3A%221AF19BF9717DA0B05A3BFC5007873E7743BA54C0311CCCCC60776AAEAC5C4635%22%2C%22binary%22%3Afalse%7D)

| Field           | JSON Type | [Internal Type][] | Description                  |
|:----------------|:----------|:------------------|:-----------------------------|
| `Account`       | String    | AccountID         | The address of the account that owns the URIToken to be burned. |
| `URITokenID`    | String    | Hash256           | The ID of the URIToken to be burned. |

## Special Transaction Cost

The URITokenBurn transaction does not have any special transaction cost requirements.

## Error Cases

Besides errors that can occur for all transactions, URITokenBurn transactions can result in the following transaction result codes:

| Error Code | Description |
|:-----------|:------------|
| `tecDUPLICATE` | Occurs if the URIToken to be burned already exists. |
| `tecDIR_FULL` | Occurs if the owner directory for the account is full and cannot accommodate the new URIToken. |
| `terNO_ACCOUNT` | Occurs if the account sending the transaction does not exist. |

