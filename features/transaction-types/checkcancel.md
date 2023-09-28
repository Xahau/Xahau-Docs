---
description: >-
  Cancels an unredeemed Check, removing it from the ledger without sending any
  money. The source or the destination of the check can cancel a Check at any
  time using this transaction type.
---

# CheckCancel

\[[Source](https://github.com/Xahau/xahaud/blob/dev/src/ripple/app/tx/impl/URIToken.cpp)]

_(Added by the \[Checks amendment]\[].)_

### Example

```json
{
    "Account": "rUn84CUYbNjRoTQ6mSW7BVJPSVJNLb1QLo",
    "TransactionType": "CheckCancel",
    "CheckID": "49647F0D748DC3FE26BDACBC57F251AADEFFF391403EC9BF87C97F67E9977FB0",
    "Fee": "12"
}
```

{% hint style="info" %}
[Query Example Tx](http://localhost:4000/tx?binary=false\&id=example\_URITokenBurn\&transaction=C53ECF838647FA5A4C780377025FEC7999AB4182590510CA461444B207AB74A9)
{% endhint %}

| Field     | JSON Type | \[Internal Type]\[] | Description                                                                        |
| --------- | --------- | ------------------- | ---------------------------------------------------------------------------------- |
| `CheckID` | String    | Hash256             | The ID of the Check ledger object to cancel, as a 64-character hexadecimal string. |

### Error Cases

* If the object identified by the `CheckID` does not exist or is not a Check, the transaction fails with the result `tecNO_ENTRY`.
* If the Check is not expired and the sender of the CheckCancel transaction is not the source or destination of the Check, the transaction fails with the result `tecNO_PERMISSION`.
