---
description: >-
  Claim Amount from a payment channel, adjust the payment channel's expiration,
  or both. This transaction can be used differently depending on the transaction
  sender's role in the specified channel:
---

# PaymentChannelClaim

[\[Source\]](https://github.com/ripple/rippled/blob/master/src/ripple/app/tx/impl/PayChan.cpp)

_Added by the \[PayChan amendment]\[]._

The **source address** of a channel can:

* Send Amount from the channel to the destination with _or without_ a signed Claim.
* Set the channel to expire as soon as the channel's `SettleDelay` has passed.
* Clear a pending `Expiration` time.
* Close a channel immediately, with or without processing a claim first. The source address cannot close the channel immediately if the channel has Amount remaining.

The **destination address** of a channel can:

* Receive Amount from the channel using a signed Claim.
* Close the channel immediately after processing a Claim, refunding any unclaimed Amount to the channel's source.

**Any address** sending this transaction can:

* Cause a channel to be closed if its `Expiration` or `CancelAfter` time is older than the previous ledger's close time. Any validly-formed PaymentChannelClaim transaction has this effect regardless of the contents of the transaction.

### Example

```json
{
  "Channel": "C1AE6DDDEEC05CF2978C0BAD6FE302948E9533691DC749DCDD3B9E5992CA6198",
  "Amount" : {
     "currency" : "USD",
     "value" : "1",
     "issuer" : "rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn"
  },
  "Signature": "30440220718D264EF05CAED7C781FF6DE298DCAC68D002562C9BF3A07C1E721B420C0DAB02203A5A4779EF4D2CCC7BC3EF886676D803A9981B928D3B8ACA483B80ECA3CD7B9B",
  "PublicKey": "32D2471DB72B27E3310F355BB33E339BF26F8392D5A93D3BC0FC3B566612DA0F0A"
}
```

| Field       | JSON Type                                                                                                                          | \[Internal Type]\[] | Description                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------- | ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Channel`   | String                                                                                                                             | Hash256             | The unique ID of the channel, as a 64-character hexadecimal string.                                                                                                                                                                                                                                                                                                                                                          |
| `Balance`   | [Currency Amount](https://docs.xahau.network/technical/protocol-reference/data-types/currency-formats#specifying-currency-amounts) | Amount              | _(Optional)_ Total amount delivered by this channel after processing this claim. Required to deliver Amount. Must be more than the total amount delivered by the channel so far, but not greater than the `Amount` of the signed claim. Must be provided except when closing the channel.                                                                                                                                    |
| `Amount`    | [Currency Amount](https://docs.xahau.network/technical/protocol-reference/data-types/currency-formats#specifying-currency-amounts) | Amount              | _(Optional)_ The amount authorized by the `Signature`. This must match the amount in the signed message. This is the cumulative amount of Amount that can be dispensed by the channel, including XAH previously redeemed.                                                                                                                                                                                                    |
| `Signature` | String                                                                                                                             | Blob                | _(Optional)_ The signature of this claim, as hexadecimal. The signed message contains the channel ID and the amount of the claim. Required unless the sender of the transaction is the source address of the channel.                                                                                                                                                                                                        |
| `PublicKey` | String                                                                                                                             | Blob                | _(Optional)_ The public key used for the signature, as hexadecimal. This must match the `PublicKey` stored in the ledger for the channel. Required unless the sender of the transaction is the source address of the channel and the `Signature` field is omitted. (The transaction includes the public key so that `rippled` can check the validity of the signature before trying to apply the transaction to the ledger.) |

If the payment channel was created before the fixPayChanRecipientOwnerDir amendment became enabled (on 2020-05-01), it is possible that the destination of the payment channel has been deleted and does not currently exist in the ledger. If the destination has been deleted, the source account cannot send XAH from the channel to the destination; instead, the transaction fails with `tecNO_DST`. (And, of course, the deleted account cannot send any transactions at all.) Other uses of this transaction type are unaffected when the destination account has been deleted, including adjusting the channel expiration, closing a channel with no Amount, or removing a channel that has passed its expiration time.

### PaymentChannelClaim Flags

Transactions of the PaymentChannelClaim type support additional values in the `Flags` field, as follows:

| Flag Name | Hex Value    | Decimal Value | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| --------- | ------------ | ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `tfRenew` | `0x00010000` | 65536         | Clear the channel's `Expiration` time. (`Expiration` is different from the channel's immutable `CancelAfter` time.) Only the source address of the payment channel can use this flag.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `tfClose` | `0x00020000` | 131072        | Request to close the channel. Only the channel source and destination addresses can use this flag. This flag closes the channel immediately if it has no more Amount allocated to it after processing the current claim, or if the destination address uses it. If the source address uses this flag when the channel still holds an Amount, this schedules the channel to close after `SettleDelay` seconds have passed. (Specifically, this sets the `Expiration` of the channel to the close time of the previous ledger plus the channel's `SettleDelay` time, unless the channel already has an earlier `Expiration` time.) If the destination address uses this flag when the channel still holds an Amount, any Amount that remains after processing the claim is returned to the source address. |
