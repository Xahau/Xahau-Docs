---
description: >-
  Add additional Amount to an open payment channel, and optionally update the
  expiration time of the channel. Only the source address of the channel can use
  this transaction.
---

# PaymentChannelFund

[\[Source\]](https://github.com/ripple/rippled/blob/master/src/ripple/app/tx/impl/PayChan.cpp)

_Added by the \[PayChan amendment]\[]._

### Example

```json
{
    "Account": "rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn",
    "TransactionType": "PaymentChannelFund",
    "Channel": "C1AE6DDDEEC05CF2978C0BAD6FE302948E9533691DC749DCDD3B9E5992CA6198",
    "Amount" : {
         "currency" : "USD",
         "value" : "1",
         "issuer" : "rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn"
      },
    "Expiration": 543171558
}
```

| Field        | JSON Type        | \[Internal Type]\[] | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------ | ---------------- | ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Channel`    | String           | Hash256             | The unique ID of the channel to fund, as a 64-character hexadecimal string.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `Amount`     | String or Object | Amount              | Amount to add to the channel. Must be a positive amount.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `Expiration` | Number           | UInt32              | _(Optional)_ New `Expiration` time to set for the channel, in \[seconds since the Ripple Epoch]\[]. This must be later than either the current time plus the `SettleDelay` of the channel, or the existing `Expiration` of the channel. After the `Expiration` time, any transaction that would access the channel closes the channel without taking its normal action. Any unspent Amount is returned to the source address when the channel closes. (`Expiration` is separate from the channel's immutable `CancelAfter` time.) For more information, see the PayChannel ledger object type. |

### Error Cases

Besides errors that can occur for all transactions, \{{currentpage.name\}} transactions can result in the following transaction result codes:

| Error Code                | Description                                                                                                                                                                                        |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `tecINSUFFICIENT_RESERVE` | The sending account has less XAH than the reserve requirement.                                                                                                                                     |
| `tecNO_DST`               | The destination account of the channel has been deleted. This is only possible if the payment channel was created before the fixPayChanRecipientOwnerDir amendment became enabled (on 2020-05-01). |
| `tecNO_ENTRY`             | The Payment Channel identified by the `Channel` field does not exist.                                                                                                                              |
| `tecNO_PERMISSION`        | The sender of the transaction is not the source address for the channel.                                                                                                                           |
| `tecUNFUNDED`             | The sending account does not have enough Amount to fund the channel with the requested amount and still meet the reserve requirement.                                                              |
| `temBAD_AMOUNT`           | The `Amount` field of the transaction is invalid. The amount cannot be zero or negative.                                                                                                           |
| `temBAD_EXPIRATION`       | The `Expiration` field is invalid.                                                                                                                                                                 |
