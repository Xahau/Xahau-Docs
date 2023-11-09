---
description: >-
  A DepositPreauth transaction gives another account pre-approval to deliver
  payments to the sender of this transaction.
---

# DepositPreauth

**Tip:** You can use this transaction to preauthorize certain counterparties before you enable Deposit Authorization. This may be useful to ensure a smooth transition from not requiring deposit authorization to requiring it.

\[[Source](https://github.com/Xahau/xahaud/blob/dev/src/ripple/app/tx/impl/URIToken.cpp)]

_Added by the \[DepositPreauth amendment]\[]._

### Example

```json
{
  "TransactionType" : "DepositPreauth",
  "Account" : "rsUiUMpnrgxQp24dJYZDhmV4bE3aBtQyt8",
  "Authorize" : "rEhxGqkqPPSxQ3P25J66ft5TwpzV14k2de",
  "Fee" : "10",
  "Flags" : 2147483648,
  "Sequence" : 2
}
```

### Fields

| Field         | JSON Type | \[Internal Type]\[] | Description                                                                      |
| ------------- | --------- | ------------------- | -------------------------------------------------------------------------------- |
| `Authorize`   | String    | AccountID           | _(Optional)_ Xahau address of the sender to preauthorize.                        |
| `Unauthorize` | String    | AccountID           | _(Optional)_ Xahau address of a sender whose preauthorization should be revoked. |

You must provide _either_ `Authorize` or `Unauthorize`, but not both.

### Error Cases

* An account cannot preauthorize (or unauthorize) its own address. Attempting to do so fails with the result `temCANNOT_PREAUTH_SELF`.
* Attempting to preauthorize an account which is already preauthorized fails with the result `tecDUPLICATE`.
* Attempting to unauthorize an account which is not preauthorized fails with the result `tecNO_ENTRY`.
* Attempting to preauthorize an address that is not funded in the ledger fails with the result `tecNO_TARGET`.
* Adding authorization adds a DepositPreauth object to the ledger, which counts toward the owner reserve requirement. If the sender of the transaction does not have enough XAH to pay for the increased reserve, the transaction fails with the result `tecINSUFFICIENT_RESERVE`. If the sender of the account is already at the maximum number of owned objects, the transaction fails with the result `tecDIR_FULL`.
