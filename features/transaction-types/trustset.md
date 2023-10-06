---
description: Create or modify a trust line linking two accounts.
---

# TrustSet

[\[Source\]](https://github.com/XRPLF/rippled/blob/master/src/ripple/app/tx/impl/SetTrust.cpp)

### Example

```json
{
    "TransactionType": "TrustSet",
    "Account": "ra5nK24KXen9AHvsdFTKHSANinZseWnPcX",
    "Fee": "12",
    "Flags": 262144,
    "LastLedgerSequence": 8007750,
    "LimitAmount": {
      "currency": "USD",
      "issuer": "rsP3mgGb2tcYUrxiLFiHJiQXhsziegtwBc",
      "value": "100"
    },
    "Sequence": 12
}
```

| Field                    | JSON Type | \[Internal Type]\[] | Description                                                                                                                                                                                   |
| ------------------------ | --------- | ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `LimitAmount`            | Object    | Amount              | Object defining the trust line to create or modify, in the format of a \[Currency Amount]\[].                                                                                                 |
| `LimitAmount`.`currency` | String    | (Amount.currency)   | The currency to this trust line applies to, as a three-letter [ISO 4217 Currency Code](https://www.xe.com/iso4217.php) or a 160-bit hex value according to currency format. "XRP" is invalid. |
| `LimitAmount`.`value`    | String    | (Amount.value)      | Quoted decimal representation of the limit to set on this trust line.                                                                                                                         |
| `LimitAmount`.`issuer`   | String    | (Amount.issuer)     | The address of the account to extend trust to.                                                                                                                                                |
| `QualityIn`              | Number    | UInt32              | _(Optional)_ Value incoming balances on this trust line at the ratio of this number per 1,000,000,000 units. A value of `0` is shorthand for treating balances at face value.                 |
| `QualityOut`             | Number    | UInt32              | _(Optional)_ Value outgoing balances on this trust line at the ratio of this number per 1,000,000,000 units. A value of `0` is shorthand for treating balances at face value.                 |

If the account specified in `LimitAmount.issuer` is blocking incoming trust lines, the transaction fails with the result code `tecNO_PERMISSION`. _(Requires the \[DisallowIncoming amendment]\[] :not\_enabled:)_

### TrustSet Flags

Transactions of the TrustSet type support additional values in the `Flags` field, as follows:

| Flag Name         | Hex Value    | Decimal Value | Description                                                                                                                                        |
| ----------------- | ------------ | ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| `tfSetfAuth`      | `0x00010000` | 65536         | Authorize the other party to hold currency issued by this account. (No effect unless using the `asfRequireAuth` AccountSet flag.) Cannot be unset. |
| `tfSetNoRipple`   | `0x00020000` | 131072        | Enable the No Ripple flag, which blocks rippling between two trust lines of the same currency if this flag is enabled on both.                     |
| `tfClearNoRipple` | `0x00040000` | 262144        | Disable the No Ripple flag, allowing rippling on this trust line.                                                                                  |
| `tfSetFreeze`     | `0x00100000` | 1048576       | Freeze the trust line.                                                                                                                             |
| `tfClearFreeze`   | `0x00200000` | 2097152       | Unfreeze the trust line.                                                                                                                           |

If a transaction tries to enable No Ripple but cannot, it fails with the result code `tecNO_PERMISSION`. Before the \[fix1578 amendment]\[] became enabled, such a transaction would result in `tesSUCCESS` (making any other changes it could) instead.

The Auth flag of a trust line does not determine whether the trust line counts towards its owner's XRP reserve requirement. However, an enabled Auth flag prevents the trust line from being in its default state. An authorized trust line can never be deleted. An issuer can pre-authorize a trust line with the `tfSetfAuth` flag only, even if the limit and balance of the trust line are 0.
