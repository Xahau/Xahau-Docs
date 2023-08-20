---
html: uritokencancelselloffer.html
title: Cancel a sell offer for a URIToken.
tags:
  - URIToken
---
# URITokenCancelSellOffer

[[Source]](https://github.com/ripple/rippled/blob/develop/src/ripple/app/tx/impl/URITokenCancelSellOffer.cpp "Source")

_(Added by the [URIToken amendment][].)_

An URITokenCancelSellOffer transaction cancels a sell offer for a [URIToken](uritoken.html) in the XRP Ledger.

## Example URITokenCancelSellOffer JSON

```json
{
    "TransactionType": "URITokenCancelSellOffer",
    "Account": "r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59",
    "URITokenID": "C1AE6DDDEEC05CF2978C0BAD6FE27362498DGS691DC749DCDD3B95992978C0BA",
}
```

[Query example transaction. >](websocket-api-tool.html?server=wss%3A%2F%2Fxrplcluster.com%2F&req=%7B%22id%22%3A%22example_URITokenCancelSellOffer%22%2C%22command%22%3A%22tx%22%2C%22transaction%22%3A%221AF19BF9717DA0B05A3BFC5007873E7743BA54C0311CCCCC60776AAEAC5C4635%22%2C%22binary%22%3Afalse%7D)

## Fields

| Field           | JSON Type | [Internal Type][] | Description                  |
|:----------------|:----------|:------------------|:-----------------------------|
| `Account`       | String    | AccountID         | The address of the account that owns the sell offer to cancel. |
| `URITokenID`    | String    | Hash256           | The ID of the URIToken to cancel the sell offer. |

## Error Cases

Besides errors that can occur for all transactions, {{currentpage.name}} transactions can result in the following [transaction result codes](transaction-results.html):

| Error Code | Description |
|:-----------|:------------|
| `tecNO_ENTRY` | Occurs if the specified sell offer does not exist. |

