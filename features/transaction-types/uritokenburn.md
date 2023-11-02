---
description: >-
  The URITokenBurn transaction is used to burn a URIToken in the XRP Ledger.
  Burning a URIToken permanently removes it from circulation.
---

# URITokenBurn

[\[Source\]](https://github.com/ripple/rippled/blob/develop/src/ripple/app/tx/impl/URIToken.cpp)

_(Added by the \[URIToken amendment]\[].)_

The URITokenBurn transaction is used to burn a URIToken in the XRP Ledger. Burning a URIToken permanently removes it from circulation.

### Example

```json
{
    "TransactionType": "URITokenBurn",
    "Account": "rWYkbWkCeg8dP6rXALnjgZSjjLyih5NXm",
    "URITokenID": "C1AE6DDDEEC05CF2978C0BAD6FE27362498DGS691DC749DCDD3B95992978C0BA",
}
```

| Field        | JSON Type | \[Internal Type]\[] | Description                                                     |
| ------------ | --------- | ------------------- | --------------------------------------------------------------- |
| `Account`    | String    | AccountID           | The address of the account that owns the URIToken to be burned. |
| `URITokenID` | String    | Hash256             | The ID of the URIToken to burn.                                 |

### Special Transaction Cost

The URITokenBurn transaction does not have any special transaction cost requirements.

### Error Cases

Besides errors that can occur for all transactions, URITokenBurn transactions can result in the following transaction result codes:

| Error Code         | Description                                                       |
| ------------------ | ----------------------------------------------------------------- |
| `tecNO_PERMISSION` | Occurs if the account does not have permission to burn the token. |

