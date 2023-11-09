---
description: >-
  An AccountDelete transaction deletes an account and any objects it owns in
  Xahau, if possible, sending the account's remaining XAH to a specified
  destination account.
---

# AccountDelete

\[[Source](https://github.com/Xahau/xahaud/blob/dev/src/ripple/app/tx/impl/DeleteAccount.cpp)]

_Added by the DeletableAccounts amendment_

### Example

```json
{
    "TransactionType": "AccountDelete",
    "Account": "rWYkbWkCeg8dP6rXALnjgZSjjLyih5NXm",
    "Destination": "rPT1Sjq2YGrBMTttX4GZHjKu9dyfzbpAYe",
    "DestinationTag": 13,
    "Fee": "2000000",
    "Sequence": 2470665,
    "Flags": 2147483648
}
```

| Field            | JSON Type              | \[Internal Type]\[] | Description                                                                                                                                                            |
| ---------------- | ---------------------- | ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Destination`    | String - \[Address]\[] | AccountID           | The address of an account to receive any leftover XAH after deleting the sending account. Must be a funded account in the ledger, and must not be the sending account. |
| `DestinationTag` | Number                 | UInt32              | _(Optional)_ Arbitrary destination tag that identifies a hosted recipient or other information for the recipient of the deleted account's leftover XAH.                |

### Special Transaction Cost

As an additional deterrent against ledger spam, the AccountDelete transaction requires a much higher than usual transaction cost: instead of the standard minimum of 0.00001 XAH, AccountDelete must destroy at least the owner reserve amount, currently 2 XRP. This discourages excessive creation of new accounts because the reserve requirement cannot be fully recouped by deleting the account.

The transaction cost always applies when a transaction is included in a validated ledger, even if the transaction fails to delete the account. (See Error Cases.) To greatly reduce the chances of paying the high transaction cost if the account cannot be deleted, submit the transaction with `fail_hard` enabled.

### Error Cases

Besides errors that can occur for all transactions, AccountDelete transactions can result in the following transaction result codes:

| Error Code           | Description                                                                                                                                                                                                                                                                                                                         |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `temDISABLED`        | Occurs if the DeletableAccounts amendment is not enabled.                                                                                                                                                                                                                                                                           |
| `temDST_IS_SRC`      | Occurs if the `Destination` matches the sender of the transaction (`Account` field).                                                                                                                                                                                                                                                |
| `tecDST_TAG_NEEDED`  | Occurs if the `Destination` account requires a destination tag, but the `DestinationTag` field was not provided.                                                                                                                                                                                                                    |
| `tecNO_DST`          | Occurs if the `Destination` account is not a funded account in the ledger.                                                                                                                                                                                                                                                          |
| `tecNO_PERMISSION`   | Occurs if the `Destination` account requires deposit authorization and the sender is not preauthorized.                                                                                                                                                                                                                             |
| `tecTOO_SOON`        | Occurs if the sender's `Sequence` number is too high. The transaction's `Sequence` number plus 256 must be less than the current \[Ledger Index]\[]. This prevents replay of old transactions if this account is resurrected after it is deleted.                                                                                   |
| `tecHAS_OBLIGATIONS` | Occurs if the account to be deleted is connected to objects that cannot be deleted in the ledger. (This includes objects created by other accounts, such as escrows and for example NFT's minted, [even if owned by another account](https://github.com/XRPLF/rippled/blob/develop/src/ripple/app/tx/impl/DeleteAccount.cpp#L197).) |
| `tefTOO_BIG`         | Occurs if the sending account is linked to more than 1000 objects in the ledger. The transaction could succeed on retry if some of those objects were deleted separately first.                                                                                                                                                     |

