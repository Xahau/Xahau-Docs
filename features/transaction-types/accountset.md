---
description: >-
  An AccountSet transaction modifies the properties of an account in the XRP
  Ledger.
---

# AccountSet

\[[Source](https://github.com/Xahau/xahaud/blob/dev/src/ripple/app/tx/impl/URIToken.cpp)]

### Example

```json
{
    "TransactionType": "AccountSet",
    "Account" : "rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn",
    "Fee": "12",
    "Sequence": 5,
    "Domain": "6578616D706C652E636F6D",
    "SetFlag": 5,
    "MessageKey": "03AB40A0490F9B7ED8DF29D246BF2D6269820A0EE7742ACDD457BEA7C7D0931EDB"
}
```



{% hint style="info" %}
[Query Example Tx](http://localhost:4000/tx?binary=false\&id=example\_URITokenBurn\&transaction=C53ECF838647FA5A4C780377025FEC7999AB4182590510CA461444B207AB74A9)
{% endhint %}

<table><thead><tr><th>Field</th><th width="137">JSON Type</th><th width="163">[Internal Type][]</th><th>Description</th></tr></thead><tbody><tr><td><code>ClearFlag</code></td><td>Number</td><td>UInt32</td><td><em>(Optional)</em> Unique identifier of a flag to disable for this account.</td></tr><tr><td><code>Domain</code></td><td>String</td><td>Blob</td><td><em>(Optional)</em> The domain that owns this account, as a string of hex representing the ASCII for the domain in lowercase. <a href="https://github.com/XRPLF/rippled/blob/55dc7a252e08a0b02cd5aa39e9b4777af3eafe77/src/ripple/app/tx/impl/SetAccount.h#L34">Cannot be more than 256 bytes in length.</a></td></tr><tr><td><code>EmailHash</code></td><td>String</td><td>Hash128</td><td><em>(Optional)</em> An arbitrary 128-bit value. Conventionally, clients treat this as the md5 hash of an email address to use for displaying a <a href="http://en.gravatar.com/site/implement/hash/">Gravatar</a> image.</td></tr><tr><td><code>MessageKey</code></td><td>String</td><td>Blob</td><td><em>(Optional)</em> Public key for sending encrypted messages to this account. To set the key, it must be exactly 33 bytes, with the first byte indicating the key type: <code>0x02</code> or <code>0x03</code> for secp256k1 keys, <code>0xED</code> for Ed25519 keys. To remove the key, use an empty value.</td></tr><tr><td><code>NFTokenMinter</code></td><td>String</td><td>Blob</td><td><em>(Optional)</em> Another account that can mint NFTokens for you. <em>(Added by the [NonFungibleTokensV1_1 amendment][].)</em></td></tr><tr><td><code>SetFlag</code></td><td>Number</td><td>UInt32</td><td><em>(Optional)</em> Integer flag to enable for this account.</td></tr><tr><td><code>TransferRate</code></td><td>Number</td><td>UInt32</td><td><em>(Optional)</em> The fee to charge when users transfer this account's tokens, represented as billionths of a unit. Cannot be more than <code>2000000000</code> or less than <code>1000000000</code>, except for the special case <code>0</code> meaning no fee.</td></tr><tr><td><code>TickSize</code></td><td>Number</td><td>UInt8</td><td><em>(Optional)</em> Tick size to use for offers involving a currency issued by this address. The exchange rates of those offers is rounded to this many significant digits. Valid values are <code>3</code> to <code>15</code> inclusive, or <code>0</code> to disable. <em>(Added by the [TickSize amendment][])</em></td></tr><tr><td><code>WalletLocator</code></td><td>String</td><td>Hash256</td><td><em>(Optional)</em> An arbitrary 256-bit value. If specified, the value is stored as part of the account but has no inherent meaning or requirements.</td></tr><tr><td><code>WalletSize</code></td><td>Number</td><td>UInt32</td><td><em>(Optional)</em> Not used. This field is valid in AccountSet transactions but does nothing.</td></tr></tbody></table>

If none of these options are provided, then the AccountSet transaction has no effect (beyond destroying the transaction cost). See Cancel or Skip a Transaction for more details.

### Domain

The `Domain` field is represented as the hex string of the lowercase ASCII of the domain. For example, the domain _example.com_ would be represented as `"6578616D706C652E636F6D"`.

To remove the `Domain` field from an account, send an AccountSet with the Domain set to an empty string.

You can put any domain in your account's `Domain` field. To prove that an account and domain belong to the same person or business, you need a "two-way link":

* Accounts you own should have a domain you own in the `Domain` field.
* At that domain, host an xrp-ledger.toml file listing accounts you own, and optionally other information about how you use the XRP Ledger.

### AccountSet Flags

There are several options which can be either enabled or disabled for an account. Account options are represented by different types of flags depending on the situation:

* The `AccountSet` transaction type has several "AccountSet Flags" (prefixed **`asf`**) that can enable an option when passed as the `SetFlag` parameter, or disable an option when passed as the `ClearFlag` parameter. Newer options have only this style of flag. You can enable up to one `asf` flag per transaction, and disable up to one `asf` flag per transaction.
* The `AccountSet` transaction type has several transaction flags (prefixed **`tf`**) that can be used to enable or disable specific account options when passed in the `Flags` parameter. You can enable and disable a combination of settings in one transaction using multiple `tf` flags, but not all settings have `tf` flags.
* The `AccountRoot` ledger object type has several ledger-state-flags (prefixed **`lsf`**) which represent the state of particular account options within a particular ledger. These settings apply until a transaction changes them.

To enable or disable Account Flags, use the `SetFlag` and `ClearFlag` parameters of an AccountSet transaction. AccountSet flags have names that begin with **`asf`**.

All flags are disabled by default.

The available AccountSet flags are:

<table><thead><tr><th width="235">Flag Name</th><th width="151">Decimal Value</th><th width="247">Corresponding Ledger Flag</th><th>Description</th></tr></thead><tbody><tr><td><code>asfAccountTxnID</code></td><td>5</td><td>(None)</td><td>Track the ID of this account's most recent transaction. Required for <code>AccountTxnID</code></td></tr><tr><td><code>asfAuthorizedNFTokenMinter</code></td><td>10</td><td>(None)</td><td>Enable to allow another account to mint non-fungible tokens (NFTokens) on this account's behalf. Specify the authorized account in the <code>NFTokenMinter</code> field of the AccountRoot object. To remove an authorized minter, enable this flag and omit the <code>NFTokenMinter</code> field. <em>(Added by the [NonFungibleTokensV1_1 amendment][].)</em></td></tr><tr><td><code>asfDefaultRipple</code></td><td>8</td><td><code>lsfDefaultRipple</code></td><td>Enable rippling on this account's trust lines by default.</td></tr><tr><td><code>asfDepositAuth</code></td><td>9</td><td><code>lsfDepositAuth</code></td><td>Enable Deposit Authorization on this account. <em>(Added by the [DepositAuth amendment][].)</em></td></tr><tr><td><code>asfDisableMaster</code></td><td>4</td><td><code>lsfDisableMaster</code></td><td>Disallow use of the master key pair. Can only be enabled if the account has configured another way to sign transactions, such as a Regular Key or a Signer List.</td></tr><tr><td><code>asfDisallowIncomingCheck</code></td><td>13</td><td><code>lsfDisallowIncomingCheck</code></td><td>Block incoming Checks. <em>(Requires the [DisallowIncoming amendment][] :not_enabled:)</em></td></tr><tr><td><code>asfDisallowIncomingNFTokenOffer</code></td><td>12</td><td><code>lsfDisallowIncomingNFTokenOffer</code></td><td>Block incoming NFTokenOffers. <em>(Requires the [DisallowIncoming amendment][] :not_enabled:)</em></td></tr><tr><td><code>asfDisallowIncomingPayChan</code></td><td>14</td><td><code>lsfDisallowIncomingPayChan</code></td><td>Block incoming Payment Channels. <em>(Requires the [DisallowIncoming amendment][] :not_enabled:)</em></td></tr><tr><td><code>asfDisallowIncomingTrustline</code></td><td>15</td><td><code>lsfDisallowIncomingTrustline</code></td><td>Block incoming trust lines. <em>(Requires the [DisallowIncoming amendment][] :not_enabled:)</em></td></tr><tr><td><code>asfDisallowXRP</code></td><td>3</td><td><code>lsfDisallowXRP</code></td><td>XRP should not be sent to this account. (Advisory; not enforced by the XRP Ledger protocol.)</td></tr><tr><td><code>asfGlobalFreeze</code></td><td>7</td><td><code>lsfGlobalFreeze</code></td><td>Freeze all assets issued by this account.</td></tr><tr><td><code>asfNoFreeze</code></td><td>6</td><td><code>lsfNoFreeze</code></td><td>Permanently give up the ability to freeze individual trust lines or disable Global Freeze. This flag can never be disabled after being enabled.</td></tr><tr><td><code>asfRequireAuth</code></td><td>2</td><td><code>lsfRequireAuth</code></td><td>Require authorization for users to hold balances issued by this address. Can only be enabled if the address has no trust lines connected to it.</td></tr><tr><td><code>asfRequireDest</code></td><td>1</td><td><code>lsfRequireDestTag</code></td><td>Require a destination tag to send transactions to this account.</td></tr></tbody></table>

To enable the `asfDisableMaster` or `asfNoFreeze` flags, you must authorize the transaction by signing it with the master key pair. You cannot use a regular key pair or a multi-signature. You can disable `asfDisableMaster` (that is, re-enable the master key pair) using a regular key pair or multi-signature.

The following Transaction flags (`tf` flags), specific to the AccountSet transaction type, serve the same purpose. Due to limited space, some settings do not have associated `tf` flags, and new `tf` flags are not being added to the `AccountSet` transaction type. You can use a combination of `tf` and `asf` flags to enable multiple settings with a single transaction.

| Flag Name           | Hex Value    | Decimal Value | Replaced by AccountSet Flag    |
| ------------------- | ------------ | ------------- | ------------------------------ |
| `tfRequireDestTag`  | `0x00010000` | 65536         | `asfRequireDest` (`SetFlag`)   |
| `tfOptionalDestTag` | `0x00020000` | 131072        | `asfRequireDest` (`ClearFlag`) |
| `tfRequireAuth`     | `0x00040000` | 262144        | `asfRequireAuth` (`SetFlag`)   |
| `tfOptionalAuth`    | `0x00080000` | 524288        | `asfRequireAuth` (`ClearFlag`) |
| `tfDisallowXRP`     | `0x00100000` | 1048576       | `asfDisallowXRP` (`SetFlag`)   |
| `tfAllowXRP`        | `0x00200000` | 2097152       | `asfDisallowXRP` (`ClearFlag`) |

**Caution:** The numeric values of `tf` and `asf` flags in transactions do not match up with the values they set in the accounts "at rest" in the ledger. To read the flags of an account in the ledger, see `AccountRoot` flags.

#### Blocking Incoming Transactions

Incoming transactions with unclear purposes may be an inconvenience for financial institutions, who would have to recognize when a customer made a mistake, and then potentially refund accounts or adjust balances depending on the mistake. The `asfRequireDest` and `asfDisallowXRP` flags are intended to protect users from accidentally sending funds in a way that is unclear about the reason the funds were sent.

For example, a destination tag is typically used to identify which hosted balance should be credited when a financial institution receives a payment. If the destination tag is omitted, it may be unclear which account should be credited, creating a need for refunds, among other problems. By using the `asfRequireDest` tag, you can ensure that every incoming payment has a destination tag, which makes it harder for others to send you an ambiguous payment by accident.

You can protect against unwanted incoming payments for non-XRP currencies by not creating trust lines in those currencies. Since XRP does not require trust, the `asfDisallowXRP` flag is used to discourage users from sending XRP to an account. However, this flag is not enforced in the XRP Ledger protocol because it could potentially cause accounts to become unusable if they run out of XRP. Instead, client applications should disallow or discourage XRP payments to accounts with the `asfDisallowXRP` flag enabled.

If you want to block _all_ incoming payments, you can enable Deposit Authorization. This prevents any transaction from sending money to you, even XRP, unless your account is below the reserve requirement.

If the \[DisallowIncoming amendment]\[] :not\_enabled: is enabled, you also have the option to block all incoming Checks, NFTokenOffers, Payment Channels, and trust lines. It is generally harmless to be on the receiving end of these objects, but they can block you from deleting your account and it can be confusing to have objects you didn't expect mixed in with the list of objects you created. To block incoming objects, use one or more of these account flags:

* `asfDisallowIncomingCheck` - for Check objects
* `asfDisallowIncomingNFTOffer` - for NFTokenOffer objects
* `asfDisallowIncomingPayChan` - for PayChannel objects
* `asfDisallowIncomingTrustline` - for RippleState (trust line) objects

When a transaction would create one of these ledger entries, if the destination account has the corresponding flag enabled, the transaction fails with the result code `tecNO_PERMISSION`. Unlike Deposit Authorization, these settings do not prevent you from receiving payments in general. Also, enabling this setting doesn't stop you from creating these types of objects yourself (unless the destination of your transaction is also using the setting, of course).

### TransferRate

The `TransferRate` field specifies a fee to charge whenever counterparties transfer the currency you issue.

In the HTTP and WebSocket APIs, the transfer fee is represented as an integer, the amount that must be sent for 1 billion units to arrive. For example, a 20% transfer fee is represented as the value `1200000000`. The value cannot be less than 1000000000. (Less than that would indicate giving away money for sending transactions, which is exploitable.) You can specify `0` as a shortcut for `1000000000`, meaning no fee.

See Transfer Fees for more information.
