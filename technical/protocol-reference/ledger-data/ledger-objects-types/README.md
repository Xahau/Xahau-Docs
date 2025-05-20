# Ledger Objects Types

## Ledger Entry Common Fields <a href="#ledger-entry-common-fields" id="ledger-entry-common-fields"></a>

[\[Source\]](https://github.com/Xahau/xahaud/blob/master/src/ripple/protocol/impl/LedgerFormats.cpp)

Every entry in a ledger's state data has the same set of common fields, plus additional fields based on the ledger entry type. Field names are case-sensitive. The common fields for all ledger entries are:

| Field                    | JSON Type | Internal Type | Required? | Description                                                                                                                                                                                                                                                                                                    |
| ------------------------ | --------- | ------------- | --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `index` or `LedgerIndex` | String    | Hash256       | No        | The unique ID for this ledger entry. In JSON, this field is represented with different names depending on the context and API method. (Note, even though this is specified as "optional" in the code, every ledger entry should have one unless it's legacy data from very early in the XRP Ledger's history.) |
| `LedgerEntryType`        | String    | UInt16        | Yes       | The type of ledger entry. Valid ledger entry types include `AccountRoot`, `Offer`, `RippleState`, and others.                                                                                                                                                                                                  |
| `Flags`                  | Number    | UInt32        | Yes       | Set of bit-flags for this ledger entry.                                                                                                                                                                                                                                                                        |
| `Remarks`                | Array     | STArray       | No        | Array of remark objects to set, update, or delete (see Remarks Format)                                                                                                                                                                                                                                         |

{% hint style="warning" %}
CautionIn JSON, the ledger entry ID is in the `index` or `LedgerIndex` field. This is not the same as a ledger index in the `ledger_index` field.
{% endhint %}
