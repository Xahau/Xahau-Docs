# Currency Formats

Xahau has two kinds of digital asset: XAH and tokens. Both types have high precision, although their formats are different.

### Comparison

The following table summarizes some of the differences between XAH and tokens in Xahau:

| XAH                                                                                  | Tokens                                                                                         |
| ------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------- |
| Has no issuer.                                                                       | Always issued by a Xahau account.                                                              |
| Specified as a string.                                                               | Specified as an object.                                                                        |
| Tracked in accounts.                                                                 | Tracked in trust lines.                                                                        |
| Can never be created; can only be destroyed.                                         | Can be issued or redeemed freely.                                                              |
| Minimum value: `0`. (Cannot be negative.)                                            | Minimum value: `-9999999999999999e80`. Minimum nonzero absolute value: `1000000000000000e-96`. |
| Maximum value `100000000000` (1011) XAH. That's `100000000000000000` (1017) "drops". | Maximum value `9999999999999999e80`.                                                           |
| Precise to the nearest "drop" (0.000001 XAH)                                         | 15 decimal digits of precision.                                                                |
| Can't be frozen.                                                                     | The issuer can freeze balances.                                                                |
| No transfer fees; XAH-to-XAH payments are always direct.                             | Can take indirect paths with each issuer charging a percentage transfer fee.                   |
| Can be used in Payment Channels and Escrow.                                          | Can be used with Payment Channels or Escrow.                                                   |

For more information, see What is XAH? and Tokens.

### Specifying Currency Amounts

Use the appropriate format for the type of currency you want to specify:

* XAH Amounts
* Token Amounts

#### XAH Amounts

To specify an amount of XAH, use a String Number indicating _drops_ of XAH, where each drop is equal to 0.000001 XAH. For example, to specify 13.1 XAH:

```
"13100000"
```

**Do not specify XAH as an object.**

XAH amounts cannot be negative.

#### Token Amounts

To specify an amount of a (fungible) token, use an Amount object. This is a JSON object with three fields:

| `Field`    | Type                   | Description                                                                                                                                                                                                                                                                                                       |
| ---------- | ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `currency` | String - Currency Code | Arbitrary currency code for the token. Cannot be XAH.                                                                                                                                                                                                                                                             |
| `value`    | String Number          | Quoted decimal representation of the amount of the token. This can include scientific notation, such as `1.23e11` meaning 123,000,000,000. Both `e` and `E` may be used. This can be negative when displaying balances, but negative values are disallowed in other contexts such as specifying how much to send. |
| `issuer`   | String                 | Generally, the account that issues this token. In special cases, this can refer to the account that holds the token instead (for example, in a Clawback transaction).                                                                                                                                             |

**Caution:** These field names are case-sensitive.

For example, to represent $153.75 US dollars issued by account `r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59`, you would specify:

```json
{
    "currency": "USD",
    "value": "153.75",
    "issuer": "r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59"
}
```

#### Specifying Without Amounts

In some cases, you need to define an asset (which could be XAH or a token) without a specific amount, such as when defining an order book in the decentralized exchange.

To describe a token without an amount, specify it as a currency object, but omit the `value` field. For example:

```json
{
  "currency": "TST",
  "issuer": "rP9jPyP5kyvFRb6ZiRghAGw5u8SGAmU4bd"
}
```

To describe XAH without an amount, specify it as a JSON object with _only_ a `currency` field. Never include an `issuer` field for XAH. For example:

```json
{
  "currency": "XAH"
}
```

### String Numbers

### XAH Precision

XAH has the same precision as a 64-bit unsigned integer where each unit is equivalent to 0.000001 XAH. It uses integer math, so that any amount less than a full drop is rounded down.

### Token Precision

Tokens can represent a wide variety of assets, including those typically measured in very small or very large denominations. This format uses significant digits and a power-of-ten exponent in a similar way to scientific notation. The format supports positive and negative significant digits and exponents within the specified range. Unlike typical floating-point representations of non-whole numbers, this format uses integer math for all calculations, so it always maintains 15 decimal digits of precision. Multiplication and division have adjustments to compensate for over-rounding in the least significant digits.

When sending token amounts in Xahau's peer-to-peer network, servers serialize the amount to a 64-bit binary value.

**Tip:** For tokens that should not be divisible at all, see Non-Fungible Tokens (NFTs).

### Currency Codes

#### Standard Currency Codes

The standard format for currency codes is a three-character string such as `USD`. This is intended for use with [ISO 4217 Currency Codes](https://www.xe.com/iso4217.php). The following rules apply:

* Currency codes must be exactly 3 ASCII characters in length. The following characters are permitted: all uppercase and lowercase letters, digits, as well as the symbols `?`, `!`, `@`, `#`, `$`, `%`, `^`, `&`, `*`, `<`, `>`, `(`, `)`, `{`, `}`, `[`, `]`, and `|`.
* Currency codes are case-sensitive.
* The currency code XAH (all-uppercase) is disallowed. Real XAH typically does not use a currency code in Xahau's protocol.

At the protocol level, this format is serialized into a 160-bit binary value starting with `0x00`.

#### Nonstandard Currency Codes

You can also use a 160-bit (40-character) hexadecimal string such as `015841551A748AD2C1F76FF6ECB0CCCD00000000` as the currency code. To prevent this from being treated as a "standard" currency code, the first 8 bits MUST NOT be `0x00`.

**Deprecated:** Some previous versions of [ripple-lib](https://github.com/XRPLF/xrpl.js) supported an "interest-bearing" or "demurraging" currency code type. These codes have the first 8 bits `0x01`. Demurraging / interest-bearing currencies are no longer supported, but you may find them in ledger data. For more information, see Demurrage.
