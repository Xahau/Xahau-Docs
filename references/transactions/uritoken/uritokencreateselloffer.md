---
permalink: uritokencreateselloffer.html
title: Create a sell offer for a URIToken.
tags:
  - URIToken
---

# URITokenCreateSellOffer

[[Source]](https://github.com/ripple/rippled/blob/develop/src/ripple/app/tx/impl/URITokenCreateSellOffer.cpp "Source")

_(Added by the [URIToken amendment][].)_

An URITokenCreateSellOffer transaction allows a user to create a sell offer for a URIToken on the XRP Ledger's decentralized exchange.

## Example URITokenCreateSellOffer JSON

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

[Query example transaction. >](websocket-api-tool.html?server=wss%3A%2F%2Fxrplcluster.com%2F&req=%7B%22id%22%3A%22example_URITokenCreateSellOffer%22%2C%22command%22%3A%22tx%22%2C%22transaction%22%3A%221AF19BF9717DA0B05A3BFC5007873E7743BA54C0311CCCCC60776AAEAC5C4635%22%2C%22binary%22%3Afalse%7D)

## Fields

| Field           | JSON Type              | [Internal Type][]    | Description                  |
|:----------------|:-----------------------|:---------------------|:-----------------------------|
| `Account`       | String                 | AccountID            | The address of the account creating the sell offer. |
| `URITokenID`    | String                 | Hash256              | The ID of the URIToken being sold. |
| `Destination`   | String                 | AccountID            | _(Optional)_ The address of the account to receive the sell offer. |
| `Amount`        | [Currency Amount][]    | Amount               | The amount of currency the account wants to receive in exchange for the URIToken. |

## Error Cases

Besides errors that can occur for all transactions, URITokenCreateSellOffer transactions can result in the following [transaction result codes](transaction-results.html):

| Error Code | Description |
|:-----------|:------------|
| `tecNO_TARGET` | Occurs if the target account does not exist. |
| `tecNO_PERMISSION` | Occurs if the account does not have permission to create a sell offer. |
| `tecINSUF_RESERVE_LINE` | Occurs if the account does not have a sufficient reserve to create a sell offer. |
| `tecINSUF_RESERVE_OFFER` | Occurs if the account does not have a sufficient reserve to create a sell offer. |
| `tecUNFUNDED_OFFER` | Occurs if the account does not have a sufficient balance to create a sell offer. |
| `tecOFFER_INVALID` | Occurs if the sell offer is invalid. |

