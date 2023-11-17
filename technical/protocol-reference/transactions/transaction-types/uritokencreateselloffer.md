---
description: >-
  An URITokenCreateSellOffer transaction allows a user to create a sell offer
  for a URIToken on Xahau's decentralized exchange.
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

### Fields

| Field         | JSON Type                                                                                                                          | \[Internal Type]\[] | Description                                                                       |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------- | ------------------- | --------------------------------------------------------------------------------- |
| `Account`     | String                                                                                                                             | AccountID           | The address of the account creating the sell offer.                               |
| `URITokenID`  | String                                                                                                                             | Hash256             | The ID of the URIToken being sold.                                                |
| `Destination` | String                                                                                                                             | AccountID           | _(Optional)_ The address of the account to receive the sell offer.                |
| `Amount`      | [Currency Amount](https://docs.xahau.network/technical/protocol-reference/data-types/currency-formats#specifying-currency-amounts) | Amount              | The amount of currency the account wants to receive in exchange for the URIToken. |

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
