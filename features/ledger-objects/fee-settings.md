# Fee Settings

[\[Source\]](https://github.com/ripple/rippled/blob/master/src/ripple/protocol/impl/LedgerFormats.cpp#L115-L120)

The `FeeSettings` object type contains the current base transaction cost and reserve amounts as determined by fee voting. Each ledger version contains **at most one** `FeeSettings` object.

### Example JSON

Example `FeeSettings` object:

```json
{
   "BaseFee": "000000000000000A",
   "Flags": 0,
   "LedgerEntryType": "FeeSettings",
   "ReferenceFeeUnits": 10,
   "ReserveBase": 20000000,
   "ReserveIncrement": 5000000,
   "XahauActivationLgrSeq": 0,
   "AccountCount": 0,
   "index": "4BC50C9B0D8515D3EAAE1E74B29A95804346C491EE1A95BF25E4AAB854A6A651"
}
```

### Fields

The `FeeSettings` object has the following fields:

<table><thead><tr><th width="192">Name</th><th width="163">JSON Type</th><th width="150">[Internal Type][]</th><th width="110">Required?</th><th>Description</th></tr></thead><tbody><tr><td><code>BaseFee</code></td><td>String</td><td>UInt64</td><td>Yes</td><td>The transaction cost of the "reference transaction" in drops of XRP as hexadecimal.</td></tr><tr><td><code>Flags</code></td><td>Number</td><td>UInt32</td><td>Yes</td><td>A bit-map of boolean flags enabled for this object. Currently, the protocol defines no flags for <code>FeeSettings</code> objects. The value is always <code>0</code>.</td></tr><tr><td><code>LedgerEntryType</code></td><td>String</td><td>UInt16</td><td>Yes</td><td>The value <code>0x0073</code>, mapped to the string <code>FeeSettings</code>, indicates that this object contains the ledger's fee settings.</td></tr><tr><td><code>ReferenceFeeUnits</code></td><td>Number</td><td>UInt32</td><td>Yes</td><td>The <code>BaseFee</code> translated into "fee units".</td></tr><tr><td><code>ReserveBase</code></td><td>Number</td><td>UInt32</td><td>Yes</td><td>The base reserve for an account in the XRP Ledger, as drops of XRP.</td></tr><tr><td><code>ReserveIncrement</code></td><td>Number</td><td>UInt32</td><td>Yes</td><td>The incremental owner reserve for owning objects, as drops of XRP.</td></tr><tr><td><code>XahauActivationLgrSeq</code></td><td>Number</td><td>UInt32</td><td>No</td><td>The ledger index where Xahau genesis was activated.</td></tr><tr><td><code>AccountCount</code></td><td>Number</td><td>UInt32</td><td>No</td><td>The number of accounts created on the Xahau network.</td></tr></tbody></table>

**Warning:** The JSON format for this ledger object type is unusual. The `BaseFee`, `ReserveBase`, and `ReserveIncrement` indicate drops of XRP but _**not**_ in the usual format for \[specifying XRP]\[Currency Amount].

If the _\[XRPFees amendment]\[]_ is enabled, the `FeeSettings` object has these fields instead:

| Name                    | JSON Type | \[Internal Type]\[] | Required? | Description                                                                                                                                     |
| ----------------------- | --------- | ------------------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| `BaseFeeDrops`          | String    | Amount              | Yes       | The transaction cost of the "reference transaction" in drops of XRP.                                                                            |
| `Flags`                 | Number    | UInt32              | Yes       | A bitmap of boolean flags enabled for this object. Currently, the protocol defines no flags for `FeeSettings` objects. The value is always `0`. |
| `LedgerEntryType`       | String    | UInt16              | Yes       | The value `0x0073`, mapped to the string `FeeSettings`, indicates that this object contains the ledger's fee settings.                          |
| `ReserveBaseDrops`      | String    | Amount              | Yes       | The base reserve for an account in the XRP Ledger, as drops of XRP.                                                                             |
| `ReserveIncrementDrops` | String    | Amount              | Yes       | The incremental owner reserve for owning objects, as drops of XRP.                                                                              |
| `XahauActivationLgrSeq` | Number    | UInt32              | No        | The ledger index where Xahau genesis was activated.                                                                                             |
| `AccountCount`          | Number    | UInt32              | No        | The number of accounts created on the Xahau network.                                                                                            |

### FeeSettings ID Format

The `FeeSettings` object ID is the hash of the `FeeSettings` space key (`0x0065`) only. This means that the ID of the `FeeSettings` object in a ledger is always:

```
4BC50C9B0D8515D3EAAE1E74B29A95804346C491EE1A95BF25E4AAB854A6A651
```
