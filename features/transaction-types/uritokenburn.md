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
    "URI": "https://example.com/token/12345",
    "Fee": "2000000",
    "Sequence": 2470665,
    "Flags": 2147483648
}
```

| Field     | JSON Type | \[Internal Type]\[] | Description                                                     |
| --------- | --------- | ------------------- | --------------------------------------------------------------- |
| `Account` | String    | AccountID           | The address of the account that owns the URIToken to be burned. |
| `URI`     | String    | VL                  | The URI of the URIToken to be burned.                           |

### Special Transaction Cost

The URITokenBurn transaction does not have any special transaction cost requirements.

### Error Cases

Besides errors that can occur for all transactions, URITokenBurn transactions can result in the following transaction result codes:

| Error Code      | Description                                                   |
| --------------- | ------------------------------------------------------------- |
| `terNO_ACCOUNT` | Occurs if the account sending the transaction does not exist. |
