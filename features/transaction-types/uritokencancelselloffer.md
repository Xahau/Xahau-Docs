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



### Fields

| Field        | JSON Type | \[Internal Type]\[] | Description                                                    |
| ------------ | --------- | ------------------- | -------------------------------------------------------------- |
| `Account`    | String    | AccountID           | The address of the account that owns the sell offer to cancel. |
| `URITokenID` | String    | Hash256             | The ID of the URIToken to cancel the sell offer.               |

### Error Cases

Besides errors that can occur for all transactions, \{{currentpage.name\}} transactions can result in the following transaction result codes:

| Error Code         | Description                                                             |
| ------------------ | ----------------------------------------------------------------------- |
| `tecNO_PERMISSION` | Occurs when the account executing the tx is not the owner of the token. |
