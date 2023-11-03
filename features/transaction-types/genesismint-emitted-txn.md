---
description: >-
  The GenesisMint transaction is used to mint new XRP and distribute it to
  multiple accounts. This transaction can only be used by the genesis account.
---

# GenesisMint - (Emitted Txn)

\[[Source](https://github.com/ripple/rippled/blob/develop/src/ripple/app/tx/impl/GenesisMint.cpp)]

_Added by the \[XahauGenesis amendment]\[] and the \[Hooks amendment]\[]_

### Example

```json
{
    "TransactionType": "GenesisMint",
    "Account": "rHb9CJAWyB4rj91VRWn96DkukG4bwdtyTh",
    "GenesisMints": [
        {
            "GenesisMint": {
                "Destination": "rPT1Sjq2YGrBMTttX4GZHjKu9dyfzbpAYe",
                "Amount": "1000000000"
            },
        }
    ]
}
```

### Fields

| Field        | JSON Type | Internal Type | Description                                                                      |
| ------------ | --------- | ------------- | -------------------------------------------------------------------------------- |
| Account      | String    | AccountID     | The address of the genesis account that will mint and distribute XRP.            |
| GenesisMints | Array     | Array         | An array of objects representing the destinations and amounts of the minted XRP. |

### GenesisMint Object

The GenesisMint transaction includes an array of objects called `GenesisMints`. Each object represents a destination account and the amount of XRP to be minted and distributed to that account.

| Field           | JSON Type | Internal Type | Description                                                                |
| --------------- | --------- | ------------- | -------------------------------------------------------------------------- |
| Destination     | String    | AccountID     | The address of the account that will receive the minted XRP.               |
| Amount          | String    | Amount        | The amount of XRP to be minted and distributed to the destination account. |
| GovernanceFlags | String    | Hash256       | _(Optional)_ The governance flags associated with the destination account. |
| GovernanceMarks | String    | Hash256       | _(Optional)_ The governance marks associated with the destination account. |

### Special Transaction Cost

The GenesisMint transaction has a standard transaction cost, which is the minimum transaction cost required for all transactions.

### Error Cases

Besides errors that can occur for all transactions, the GenesisMint transaction can result in the following transaction result codes:

| Error Code     | Description                                                                                |
| -------------- | ------------------------------------------------------------------------------------------ |
| `temDISABLED`  | Occurs if the "Hooks" or "XahauGenesis" amendments are not enabled.                        |
| `temMALFORMED` | Occurs if the transaction is malformed, such as missing required fields or invalid values. |
