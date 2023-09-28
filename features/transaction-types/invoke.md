---
description: An Invoke transaction is used to trigger and interact with a hook.
---

# Invoke

\[[Source](https://github.com/Xahau/xahaud/blob/dev/src/ripple/app/tx/impl/URIToken.cpp)]

_(Added by the \[Hooks amendment]\[].)_

### Example

```json
{
  "TransactionType": "Invoke",
  "Account": "rUn84CUYbNjRoTQ6mSW7BVJPSVJNLb1QLo",
  "Destination" : "r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59"
}
```

{% hint style="info" %}
[Query Example Tx](http://localhost:4000/tx?binary=false\&id=example\_URITokenBurn\&transaction=C53ECF838647FA5A4C780377025FEC7999AB4182590510CA461444B207AB74A9)
{% endhint %}

### Fields

| Field            | JSON Type | \[Internal Type]\[] | Description                                                                                              |
| ---------------- | --------- | ------------------- | -------------------------------------------------------------------------------------------------------- |
| `Blob`           | String    | Blob                | Hex value that can represent anything and be read in the hook.                                           |
| `Destination`    | String    | AccountID           | (Optional) The unique address of the hook account that you want to invoke.                               |
| `DestinationTag` | String    | UInt32              | (Optional) Arbitrary tag that identifies the reason for the Invoke, or which recipient to interact with. |
| `InvoiceID`      | String    | Hash256             | (Optional) Arbitrary 256-bit hash representing a specific reason or identifier for this Invoke.          |

### Error Cases

* If the `Blob` is not a hex value then the transaction fails with the result code `temMALFORMED`,
* If the `Blob` is larger than 128\*1024 then the transaction fails with the result code `temMALFORMED`,
* If the `Destination` is the sender of the transaction, the transaction fails with the result code `temREDUNDANT`.
* If the `Destination` account does not exist in the ledger, the transaction fails with the result code `tecNO_DST`.
* If the `Destination` account has the `RequireDest` flag enabled but the transaction does not include a `DestinationTag` field, the transaction fails with the result code `tecDST_TAG_NEEDED`.

### Notes

* TicketSequence is not available on `Invoke`
