---
description: >-
  Attempts to redeem a Check object in the ledger to receive up to the amount
  authorized by the corresponding CheckCreate transaction.
---

# CheckCash

\[[Source](https://github.com/Xahau/xahaud/blob/dev/src/ripple/app/tx/impl/URIToken.cpp)]

_(Added by the \[Checks amendment]\[].)_

### Example

```json
{
    "Account": "rfkE1aSy9G8Upk4JssnwBxhEv5p4mn2KTy",
    "TransactionType": "CheckCash",
    "Amount": "100000000",
    "CheckID": "838766BA2B995C00744175F69A1B11E32C3DBC40E64801A4056FCBD657F57334",
    "Fee": "12"
}
```

{% hint style="info" %}
[Query Example Tx](http://localhost:4000/tx?binary=false\&id=example\_URITokenBurn\&transaction=C53ECF838647FA5A4C780377025FEC7999AB4182590510CA461444B207AB74A9)
{% endhint %}

| Field        | JSON Type             | \[Internal Type]\[] | Description                                                                                                                                                                                                                     |
| ------------ | --------------------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `CheckID`    | String                | Hash256             | The ID of the Check ledger object to cash, as a 64-character hexadecimal string.                                                                                                                                                |
| `Amount`     | \[Currency Amount]\[] | Amount              | _(Optional)_ Redeem the Check for exactly this amount, if possible. The currency must match that of the `SendMax` of the corresponding CheckCreate transaction. You must provide either this field or `DeliverMin`.             |
| `DeliverMin` | \[Currency Amount]\[] | Amount              | _(Optional)_ Redeem the Check for at least this amount and for as much as possible. The currency must match that of the `SendMax` of the corresponding CheckCreate transaction. You must provide either this field or `Amount`. |

The transaction _**must**_ include either `Amount` or `DeliverMin`, but not both.

### Error Cases

* If the sender of the CheckCash transaction is not the `Destination` of the check, the transaction fails with the result code `tecNO_PERMISSION`.
* If the Check identified by the `CheckID` field does not exist, the transaction fails with the result `tecNO_ENTRY`.
* If the Check identified by the `CheckID` field has already expired, the transaction fails with the result `tecEXPIRED`.
* If the destination of the Check has the `RequireDest` flag enabled but the Check, as created, does not have a destination tag, the transaction fails with the result code `tecDST_TAG_NEEDED`.
* If the transaction specifies both `Amount` and `DeliverMin`, or omits both, the transaction fails with the result `temMALFORMED`.
* If the `Amount` or `DeliverMin` does not match the currency (and issuer, if not XRP) of the Check, the transaction fails with the result `temBAD_CURRENCY`.
