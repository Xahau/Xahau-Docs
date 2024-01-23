---
description: Return escrowed XAH or IOU to the sender.
---

# EscrowCancel

\[[Source](https://github.com/Xahau/xahaud/blob/dev/src/ripple/app/tx/impl/URIToken.cpp)]

_Added by the \[Escrow amendment]\[]._

### Cancel Using OfferSequence

```json
{
    "Account": "rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn",
    "TransactionType": "EscrowCancel",
    "Owner": "rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn",
    "OfferSequence": 7,
}
```

### Cancel Using EscrowID

```json
{
    "Account": "rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn",
    "TransactionType": "EscrowCancel",
    "Owner": "rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn",
    "EscrowID": "49647F0D748DC3FE26BDACBC57F251AADEFFF391403EC9BF87C97F67E9977FB0",
}
```

### Fields

| Field           | JSON Type | \[Internal Type]\[] | Description                                                                                                               |
| --------------- | --------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| `Owner`         | String    | AccountID           | Address of the source account that funded the escrow payment.                                                             |
| `OfferSequence` | Number    | UInt32              | _(Optional)_ Transaction sequence (or Ticket number) of \[EscrowCreate transaction]\[] that created the escrow to cancel. |
| `EscrowID`      | String    | Hash256             | _(Optional)_ The ID of the Escrow ledger object to cancel, as a 64-character hexadecimal string.                          |

Any account may submit an EscrowCancel transaction.

* If the corresponding \[EscrowCreate transaction]\[] did not specify a `CancelAfter` time, the EscrowCancel transaction fails.
* Otherwise the EscrowCancel transaction fails if the `CancelAfter` time is after the close time of the most recently-closed ledger.
