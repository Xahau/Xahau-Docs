---
description: >-
  The Remit transaction allows the user to send multiple payment types, mint a
  URIToken, transfer a list of URITokens and activate an account.
---

# Remit

{% hint style="warning" %}
The Remit transaction pays all fees for _Account Activation, Trustlines and URIToken Reserves._
{% endhint %}

\[[Source](https://github.com/Xahau/xahaud/blob/dev/src/ripple/app/tx/impl/Remit.cpp)]

_(Added by the \[Remit amendment]\[].)_

### Example

```json
{
    "TransactionType": "Remit",
    "Account": "rGvbdrdCxG2tk9ZU2673XmsjRdHCDQEpt7",
    "Amounts": [
        {
            "AmountEntry": {
                "Amount": "1000000"
            }
        }, {
            "AmountEntry": {
                "Amount": {
                    "currency": "USD",
                    "issuer": "rExKpRKXNz25UAjbckCRtQsJFcSfjL9Er3",
                    "value": "1"
                }
            }
        }
    ],
    "Destination": "rG1QQv2nh2gr7RCZ1P8YYcBUKCCN633jCn",
    "URITokenIDs": [
        "714F206C865D334721B2F3388BEAF33AA91BC1D78C71941D10A2A653C873EDD3"
    ],
    "MintURIToken": {
        "Digest": "6F11A4DF4EE794E2800BB361173D454BFBECB3D7506C4F4CB0EC5AE98BE43747",
        "Flags": 1,
        "URI": "697066733A2F2F"
    }
}
```

<table><thead><tr><th width="228">Field</th><th>JSON Type</th><th>[Internal Type][]</th><th>Description</th></tr></thead><tbody><tr><td><code>Account</code></td><td>String</td><td>AccountID</td><td>The address of the account that will activate the account, send the payment and/or mint/transfer the URIToken/s.</td></tr><tr><td><code>Destination</code></td><td>String</td><td>AccountID</td><td>The unique address of the account receiving the payment and/or URIToken/s.</td></tr><tr><td><code>DestinationTag</code></td><td>Number</td><td>UInt32</td><td><em>(Optional)</em> A DestinationTag for deposits to a shared custody account.</td></tr><tr><td><code>MintURIToken</code></td><td>Object</td><td>STObject</td><td><em>(Optional)</em> A <code>MintURIToken</code> STObject containing the URIToken details you want to mint.</td></tr><tr><td><code>URITokenIDs</code></td><td>Array</td><td>STArray</td><td><em>(Optional)</em> An array of URITokenIDs to to be transferred to the <code>Destination</code>.</td></tr><tr><td><code>Amounts</code></td><td>Array</td><td>STArray</td><td><em>(Optional)</em> An array of <code>AmountEntry</code> STObjects the account wants to send to the <code>Destination</code>.</td></tr><tr><td><code>Inform</code></td><td>String</td><td>AccountID</td><td><em>(Optional)</em> A unique address of an account that can have a hook installed and be informed when a remit occurs.</td></tr><tr><td><code>Blob</code></td><td>String</td><td>Blob</td><td><em>(Optional)</em> Arbitrary hex value that can be added to the tx for use in Hooks.</td></tr><tr><td><code>InvoiceID</code></td><td>String</td><td>Hash256</td><td><em>(Optional)</em> Arbitrary 256-bit hash representing a specific reason or identifier for this remit.</td></tr></tbody></table>

### AmountEntry Fields

| Field    | JSON Type                                                                                                                          | \[Internal Type]\[] | Description                                                            |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------- | ------------------- | ---------------------------------------------------------------------- |
| `Amount` | [Currency Amount](https://docs.xahau.network/technical/protocol-reference/data-types/currency-formats#specifying-currency-amounts) | Amount              | The amount of currency the account wants to send to the `Destination`. |

### MintURIToken Fields

| Field    | JSON Type | \[Internal Type]\[] | Description                                                 |
| -------- | --------- | ------------------- | ----------------------------------------------------------- |
| `URI`    | String    | String              | The URI associated with the minted URIToken. (256 byte max) |
| `Digest` | String    | Hash256             | _(Optional)_ The digest of the URIToken.                    |
| `Flags`  | Number    | UInt32              | _(Optional)_ Flags on the mint transaction                  |

### MintURIToken Flags

The `MintURIToken` STObject supports the values in the `Flags` field, as follows:

| Flag Name    | Hex Value    | Decimal Value | Description                                                                                     |
| ------------ | ------------ | ------------- | ----------------------------------------------------------------------------------------------- |
| `tfBurnable` | `0x00000001` | 1             | Allow the issuer to destroy the minted `URIToken`. (The `URIToken`'s owner can _always_ do so.) |

### Special Transaction Cost

The Remit transaction has a standard transaction cost, which is the minimum fee required for any transaction in Xahau.

In addition to the minimum fee required the Remit transaction will also deduct the fees for the following:

| Action               | Fee                          |
| -------------------- | ---------------------------- |
| `Account Activation` | Standard Reserve Requirement |
| `Create Trustline`   | Standard Reserve Requirement |
| `URIToken Mint`      | Standard Reserve Requirement |
| `URIToken Transfer`  | Standard Reserve Requirement |

### Error Cases

Besides errors that can occur for all transactions, Remit transactions can result in the following transaction result codes:

| Error Code                     | Description                                                                                                                                        |
| ------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| `temINVALID_FLAG`              | Occurs if any flag is specific `tfFullyCanonicalSig`                                                                                               |
| `temREDUNDANT`                 | Occurs if the Account is the same as the Destination                                                                                               |
| `temMALFORMED (Inform & Blob)` | Occurs when; sfInform is same as " "source or destination. Blob was more than 128kib.                                                              |
| `temMALFORMED (AmountEntry)`   | Occurs when; AmountEntry count exceeds `32.` Expected AmountEntry. Native Currency appears more than once. Issued Currency appears more than once. |
| `temMALFORMED (MintURIToken)`  | Occurs when; sfMintURIToken contains invalid field. URI was not provided. URI was too long/short. Invalid UTF8 inside MintURIToken.                |
| `temMALFORMED (URITokenIDs)`   | Occurs when; URITokenIDs too short/long. Duplicate URITokenID.                                                                                     |
| `temBAD_AMOUNT`                | Occurs when an Amount in the AmountEntry is invalid.                                                                                               |
| `terNO_ACCOUNT`                | Occurs when the source account does not exist.                                                                                                     |
| `tecNO_TARGET`                 | Occurs when the `sfInform` field is present but the account does not exist.                                                                        |
| `tecNO_PERMISSION`             | Occurs when `disallowIncomingRemit` is enabled on the `Destination`                                                                                |
| `tecNO_PERMISSION`             | Occurs when the `Destination` has `DepositAuthorization` enabled.                                                                                  |
| `tecDST_TAG_NEEDED`            | Occurs if the destination account requires a destination tag, but the transaction does not include one.                                            |
| `tecDUPLICATE`                 | Occurs when the `MintURIToken` URI already exists.                                                                                                 |
| `tecDIR_FULL`                  | Occurs when the source or destination accouts directory is full.                                                                                   |
| `tecNO_ENTRY`                  | Occurs when the URIToken does not exist.                                                                                                           |
| `tecNO_PERMISSION`             | Occurs when the URIToken is not owned by the source account.                                                                                       |
| `tecUNFUNDED_PAYMENT`          | Occurs when the source account does not have the required funds to execute the transaction. (XAH or Issued Currencies)                             |
