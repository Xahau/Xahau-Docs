---
description: >-
  An URIToken Mint transaction mints a new URIToken and assigns ownership to the
  specified account. The URIToken represents a unique digital asset that can be
  used in various applications.
---

# URITokenMint

\[[Source](https://github.com/Xahau/xahaud/blob/dev/src/ripple/app/tx/impl/URIToken.cpp)]

_(Added by the \[URIToken amendment]\[].)_

### Example

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



| Field         | JSON Type             | \[Internal Type]\[] | Description                                                                                    |
| ------------- | --------------------- | ------------------- | ---------------------------------------------------------------------------------------------- |
| `Account`     | String                | AccountID           | The address of the account that will own the minted URIToken.                                  |
| `URI`         | String                | String              | The URI associated with the minted URIToken.                                                   |
| `Digest`      | String                | Hash256             | _(Optional)_ The digest of the URIToken.                                                       |
| `Destination` | String                | AccountID           | _(Optional)_ The address of the account that can buy the minted URIToken.                      |
| `Amount`      | \[Currency Amount]\[] | Amount              | _(Optional)_ The amount of currency the account wants to receive in exchange for the URIToken. |

### URITokenMint Flags

Transactions of the URITokenMint type support additional values in the `Flags` field, as follows:

| Flag Name    | Hex Value    | Decimal Value | Description                                                                                                                             |
| ------------ | ------------ | ------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| `tfBurnable` | `0x00000001` | 1             | Allow the issuer (or an entity authorized by the issuer) to destroy the minted `URIToken`. (The `URIToken`'s owner can _always_ do so.) |

### Error Cases

### Special Transaction Cost

The URIToken Mint transaction has a standard transaction cost, which is the minimum transaction cost required for all transactions.

### Error Cases

Besides errors that can occur for all transactions, URIToken Mint transactions can result in the following transaction result codes:

| Error Code        | Description                                                                      |
| ----------------- | -------------------------------------------------------------------------------- |
| `tecDUPLICATE`    | Occurs if a URIToken with the same URI already exists.                           |
| `tecDIR_FULL`     | Occurs if the owner's directory is full and cannot accommodate the new URIToken. |
| `temINVALID_FLAG` | Occurs when the user specified an incorrect `Flag`.                              |
| `terNO_ACCOUNT`   | Occurs if the sending account does not exist.                                    |
