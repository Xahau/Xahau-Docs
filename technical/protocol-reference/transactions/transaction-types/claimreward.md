---
description: >-
  A ClaimReward transaction allows an account to claim the rewards it has
  accumulated. The rewards can be claimed by the account owner or by a specified
  issuer. The account can also opt-out of rewards.
---

# ClaimReward

\[[Source](https://github.com/Xahau/xahaud/blob/dev/src/ripple/app/tx/impl/ClaimReward.cpp)]

_(Added by the \[BalanceRewards amendment]\[].)_

### Example

```json
{
    "TransactionType": "ClaimReward",
    "Account": "rWYkbWkCeg8dP6rXALnjgZSjjLyih5NXm",
    "Issuer": "rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn"
}
```

### Fields

| Field     | JSON Type | \[Internal Type]\[] | Description                                                     |
| --------- | --------- | ------------------- | --------------------------------------------------------------- |
| `Account` | String    | AccountID           | The address of the account that is claiming the reward.         |
| `Flags`   | Number    | UInt32              | _(Optional)_ Can have flag 1 set to opt-out of rewards.         |
| `Issuer`  | String    | AccountID           | _(Optional)_ The address of the account that issued the reward. |

### ClaimReward Flags

Transactions of the ClaimReward type support additional values in the `Flags` field, as follows:

| Flag Name  | Hex Value    | Decimal Value | Description                                                                                                                                                                                                           |
| ---------- | ------------ | ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `tfOptOut` | `0x00000001` | 1             | The `isOptOut` flag in the ClaimReward code is used to opt-out an account from rewards by removing reward-related fields from the account object in the ledger if the `sfFlags` field in the transaction is set to 1. |

### Special Transaction Cost

The ClaimReward transaction has a standard transaction cost, which is the minimum transaction cost required for all transactions.

### Error Cases

Besides errors that can occur for all transactions, ClaimReward transactions can result in the following transaction result codes:

| Error Code        | Description                                                                                             |
| ----------------- | ------------------------------------------------------------------------------------------------------- |
| `temDISABLED`     | Occurs if the feature is not enabled.                                                                   |
| `temINVALID_FLAG` | Occurs if the flag is set to a value other than 1.                                                      |
| `temMALFORMED`    | Occurs if the issuer is the same as the source account or if the flag and issuer are not correctly set. |
| `tecNO_ISSUER`    | Occurs if the issuer does not exist.                                                                    |
| `terNO_ACCOUNT`   | Occurs if the sending account does not exist.                                                           |
