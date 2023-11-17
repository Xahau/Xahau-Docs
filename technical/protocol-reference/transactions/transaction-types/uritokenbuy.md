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
    "Amount": {
      "issuer": "rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn",
      "currency": "USD",
      "value": "100",
    },
}
```

| Field        | JSON Type                                                                                                                          | \[Internal Type]\[] | Description                                         |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------------- | ------------------- | --------------------------------------------------- |
| `Account`    | String                                                                                                                             | AccountID           | The address of the buyer's account.                 |
| `URITokenID` | String                                                                                                                             | Hash256             | The unique identifier of the URIToken to be bought. |
| `Amount`     | [Currency Amount](https://docs.xahau.network/technical/protocol-reference/data-types/currency-formats#specifying-currency-amounts) | Amount              | The amount of currency to pay for the URIToken.     |

### Special Transaction Cost

The URITokenBuy transaction has a standard transaction cost, which is the minimum fee required for any transaction in Xahau.

### Error Cases

Besides errors that can occur for all transactions, URITokenBuy transactions can result in the following transaction result codes:

| Error Code                         | Description                                                                                                                  |
| ---------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `tecCANT_ACCEPT_OWN_NFTOKEN_OFFER` | Occurs if the owner of the token is the one claiming the offer.                                                              |
| `tecDST_TAG_NEEDED`                | Occurs if the destination account requires a destination tag, but the transaction does not include one.                      |
| `tecNO_PERMISSION`                 | Occurs if the seller does not have the token listed for sale or the token `Destination` is not the account buying the token. |
| `temBAD_CURRENCY`                  | Occurs when the buying currency does not match the offer currency.                                                           |
| `tecINSUFFICIENT_PAYMENT`          | Occurs when the buy amount is less than the offer amount.                                                                    |
| `tecINSUFFICIENT_FUNDS`            | Occurs when the buyer doesn't have sufficient funds including the `Fee` to purchase the token.                               |
