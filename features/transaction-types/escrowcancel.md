---
description: Return escrowed XRP to the sender.
---

# EscrowCancel

\[[Source](https://github.com/Xahau/xahaud/blob/dev/src/ripple/app/tx/impl/URIToken.cpp)]

_Added by the \[Escrow amendment]\[]._

### Example

```json
{
    "Account": "rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn",
    "TransactionType": "EscrowCancel",
    "Owner": "rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn",
    "OfferSequence": 7,
}
```

{% hint style="info" %}
[Query Example Tx](http://localhost:4000/tx?binary=false\&id=example\_URITokenBurn\&transaction=C53ECF838647FA5A4C780377025FEC7999AB4182590510CA461444B207AB74A9)
{% endhint %}

### Fields

| Field           | JSON Type | \[Internal Type]\[] | Description                                                                                                  |
| --------------- | --------- | ------------------- | ------------------------------------------------------------------------------------------------------------ |
| `Owner`         | String    | AccountID           | Address of the source account that funded the escrow payment.                                                |
| `OfferSequence` | Number    | UInt32              | Transaction sequence (or Ticket number) of \[EscrowCreate transaction]\[] that created the escrow to cancel. |

Any account may submit an EscrowCancel transaction.

* If the corresponding \[EscrowCreate transaction]\[] did not specify a `CancelAfter` time, the EscrowCancel transaction fails.
* Otherwise the EscrowCancel transaction fails if the `CancelAfter` time is after the close time of the most recently-closed ledger.
