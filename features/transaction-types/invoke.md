---
description: >-
  An Invoke transaction is used to call a hook, which is a piece of code that is
  executed in response to certain ledger operations.
---

# Invoke

\[[Source](https://github.com/ripple/rippled/blob/develop/src/ripple/app/tx/impl/Invoke.cpp)]

_(Added by the \[Hooks amendment]\[].)_

### Example

```json
{
    "TransactionType": "Invoke",
    "Account": "rWYkbWkCeg8dP6rXALnjgZSjjLyih5NXm",
    "Blob": "697066733A2F2F4445414442454546",
    "Destination": "rPT1Sjq2YGrBMTttX4GZHjKu9dyfzbpAYe"
}
```

| Field         | JSON Type | \[Internal Type]\[] | Description                                                                                        |
| ------------- | --------- | ------------------- | -------------------------------------------------------------------------------------------------- |
| `Account`     | String    | AccountID           | The address of the account that is invoking the hook.                                              |
| `Blob`        | String    | Blob                | _(Optional)_ A blob of data that is passed to the hook.                                            |
| `Destination` | String    | AccountID           | _(Optional)_ The address of the account that is the target of the hook.                            |
| `InvoiceID`   | String    | Hash256             | _(Optional)_ Arbitrary 256-bit hash representing a specific reason or identifier for this payment. |

### Special Transaction Cost

The Invoke transaction has a standard transaction cost, plus an additional cost based on the size of the Blob and HookParameters fields.

### Error Cases

Besides errors that can occur for all transactions, Invoke transactions can result in the following transaction result codes:

| Error Code      | Description                                                              |
| --------------- | ------------------------------------------------------------------------ |
| `temDISABLED`   | Occurs if the Hooks amendment is not enabled.                            |
| `temMALFORMED`  | Occurs if the Blob field is larger than 128 KiB.                         |
| `terNO_ACCOUNT` | Occurs if the sending account or the destination account does not exist. |
