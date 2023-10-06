---
description: >-
  The URITokenBuy transaction allows a user to buy a URIToken from the issuer.
  This transaction is used to transfer ownership of a URIToken from the issuer
  to the buyer.
---

# URITokenBuy

\[[Source](https://github.com/Xahau/xahaud/blob/dev/src/ripple/app/tx/impl/URIToken.cpp)]

_(Added by the \[URIToken amendment]\[].)_

### Example

```json
{
    "TransactionType": "URITokenBuy",
    "Account": "rWYkbWkCeg8dP6rXALnjgZSjjLyih5NXm",
    "URITokenID": "C1AE6DDDEEC05CF2978C0BAD6FE27362498DGS691DC749DCDD3B95992978C0BA",
    "Destination": "rPT1Sjq2YGrBMTttX4GZHjKu9dyfzbpAYe",
    "Amount": {
      "issuer": "rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn",
      "currency": "USD",
      "value": "100",
    },
}
```

| Field         | JSON Type             | \[Internal Type]\[] | Description                                                                                                               |
| ------------- | --------------------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| `Account`     | String                | AccountID           | The address of the buyer's account.                                                                                       |
| `URITokenID`  | String                | Hash256             | The unique identifier of the URIToken to be bought.                                                                       |
| `Amount`      | \[Currency Amount]\[] | Amount              | The amount of currency to pay for the URIToken.                                                                           |
| `Destination` | String                | AccountID           | _(Optional)_ The address of the account to receive the URIToken. If omitted, the URIToken is sent to the buyer's account. |

### Special Transaction Cost

The URITokenBuy transaction has a standard transaction cost, which is the minimum fee required for any transaction in the XRP Ledger.

### Error Cases

Besides errors that can occur for all transactions, URITokenBuy transactions can result in the following transaction result codes:

| Error Code          | Description                                                                                             |
| ------------------- | ------------------------------------------------------------------------------------------------------- |
| `tecNO_DST`         | Occurs if the destination account does not exist.                                                       |
| `tecDST_TAG_NEEDED` | Occurs if the destination account requires a destination tag, but the transaction does not include one. |
| `tecNO_PERMISSION`  | Occurs if the destination account requires deposit authorization and the buyer is not preauthorized.    |
| `terNO_ACCOUNT`     | Occurs if the buyer's account does not exist.                                                           |
| `tecDIR_FULL`       | Occurs if the owner directory of the buyer's account is full and cannot accommodate the new URIToken.   |
| `tesSUCCESS`        | Indicates a successful transaction.                                                                     |
