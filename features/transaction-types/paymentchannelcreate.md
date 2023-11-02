---
description: >-
  Create a payment channel and fund it with an Amount. The address sending this
  transaction becomes the "source address" of the payment channel.
---

# PaymentChannelCreate

[\[Source\]](https://github.com/XRPLF/rippled/blob/master/src/ripple/app/tx/impl/PayChan.cpp)

_Added by the \[PayChan amendment]\[]._

### Example

```json
{
    "Account": "rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn",
    "TransactionType": "PaymentChannelCreate",
    "Amount": "10000",
    "Destination": "rsA2LpzuawewSBQXkiju3YQTMzW13pAAdW",
    "SettleDelay": 86400,
    "PublicKey": "32D2471DB72B27E3310F355BB33E339BF26F8392D5A93D3BC0FC3B566612DA0F0A",
    "CancelAfter": 533171558,
    "DestinationTag": 23480,
    "SourceTag": 11747
}
```

| Field            | JSON Type | \[Internal Type]\[] | Description                                                                                                                                                                                                                                                                                                                   |
| ---------------- | --------- | ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Amount`         | String    | Amount              | Amount to deduct from the sender's balance and set aside in this channel. While the channel is open, the Amount can only go to the `Destination` address. When the channel closes, any unclaimed Amount is returned to the source address's balance.                                                                          |
| `Destination`    | String    | AccountID           | Address to receive claims against this channel. This is also known as the "destination address" for the channel. Cannot be the same as the sender (`Account`).                                                                                                                                                                |
| `SettleDelay`    | Number    | UInt32              | Amount of time the source address must wait before closing the channel if it has unclaimed Amount.                                                                                                                                                                                                                            |
| `PublicKey`      | String    | Blob                | The 33-byte public key of the key pair the source will use to sign claims against this channel, in hexadecimal. This can be any secp256k1 or Ed25519 public key. For more information on key pairs, see Key Derivation                                                                                                        |
| `CancelAfter`    | Number    | UInt32              | _(Optional)_ The time, in \[seconds since the Ripple Epoch]\[], when this channel expires. Any transaction that would modify the channel after this time closes the channel without otherwise affecting it. This value is immutable; the channel can be closed earlier than this time but cannot remain open after this time. |
| `DestinationTag` | Number    | UInt32              | _(Optional)_ Arbitrary tag to further specify the destination for this payment channel, such as a hosted recipient at the destination address.                                                                                                                                                                                |

If the `Destination` account is blocking incoming payment channels, the transaction fails with result code `tecNO_PERMISSION`. _(Requires the \[DisallowIncoming amendment]\[] :not\_enabled:)_
