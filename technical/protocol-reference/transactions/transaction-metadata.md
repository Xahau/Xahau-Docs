# Transaction Metadata

Transaction metadata is a section of data that gets added to a transaction after it is processed. Any transaction that gets included in a ledger has metadata, regardless of whether it is successful. The transaction metadata describes the outcome of the transaction in detail.

**Warning:** The changes described in transaction metadata are only final if the transaction is in a validated ledger version.

Some fields that may appear in transaction metadata include:

### Example Metadata

The following JSON object shows the metadata for [a complex cross-currency payment](https://xrpcharts.ripple.com/#/transactions/8C55AFC2A2AA42B5CE624AEECDB3ACFDD1E5379D4E5BF74A8460C5E97EF8706B):

```json

<div data-gb-custom-block data-tag="include" data-0='_api-examples/metadata/cross-currency-payment.json'></div>

```

### AffectedNodes

The `AffectedNodes` array contains a complete list of the objects in the ledger that this transaction modified in some way. Each entry in this array is an object with one top-level field indicating what type it is:

* `CreatedNode` indicates that the transaction created a new object in the ledger.
* `DeletedNode` indicates that the transaction removed an object from the ledger.
* `ModifiedNode` indicates that the transaction modified an existing object in the ledger.

The value of each of these fields is a JSON object describing the changes made to the ledger object.

#### CreatedNode Fields

A `CreatedNode` object contains the following fields:

| Field             | Value               | Description                                                                                                                                                |
| ----------------- | ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `LedgerEntryType` | String              | The type of ledger object that was created.                                                                                                                |
| `LedgerIndex`     | String - \[Hash]\[] | The ID of this ledger object in the ledger's state tree. **Note:** This is **not the same** as a ledger index, even though the field name is very similar. |
| `NewFields`       | Object              | The content fields of the newly-created ledger object. Which fields are present depends on what type of ledger object was created.                         |

#### DeletedNode Fields

A `DeletedNode` object contains the following fields:

| Field             | Value               | Description                                                                                                                                                |
| ----------------- | ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `LedgerEntryType` | String              | The type of ledger object that was deleted.                                                                                                                |
| `LedgerIndex`     | String - \[Hash]\[] | The ID of this ledger object in the ledger's state tree. **Note:** This is **not the same** as a ledger index, even though the field name is very similar. |
| `FinalFields`     | Object              | The content fields of the ledger object immediately before it was deleted. Which fields are present depends on what type of ledger object was created.     |

#### ModifiedNode Fields

A `ModifiedNode` object contains the following fields:

| Field               | Value                       | Description                                                                                                                                                                                                                                                                              |
| ------------------- | --------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `LedgerEntryType`   | String                      | The type of ledger object that was deleted.                                                                                                                                                                                                                                              |
| `LedgerIndex`       | String - \[Hash]\[]         | The ID of this ledger object in the ledger's state tree. **Note:** This is **not the same** as a ledger index, even though the field name is very similar.                                                                                                                               |
| `FinalFields`       | Object                      | The content fields of the ledger object after applying any changes from this transaction. Which fields are present depends on what type of ledger object was created. This omits the `PreviousTxnID` and `PreviousTxnLgrSeq` fields, even though most types of ledger objects have them. |
| `PreviousFields`    | Object                      | The previous values for all fields of the object that were changed as a result of this transaction. If the transaction _only added_ fields to the object, this field is an empty object.                                                                                                 |
| `PreviousTxnID`     | String - \[Hash]\[]         | _(May be omitted)_ The \[identifying hash]\[] of the previous transaction to modify this ledger object. Omitted for ledger object types that do not have a `PreviousTxnID` field.                                                                                                        |
| `PreviousTxnLgrSeq` | Number - \[Ledger Index]\[] | _(May be omitted)_ The \[Ledger Index]\[] of the ledger version containing the previous transaction to modify this ledger object. Omitted for ledger object types that do not have a `PreviousTxnLgrSeq` field.                                                                          |

**Note:** If the modified ledger object has `PreviousTxnID` and `PreviousTxnLgrSeq` fields, the transaction always updates them with the transaction's own identifying hash and the index of the ledger version that included the transaction, but these fields' new value is not listed in the `FinalFields` of the `ModifiedNode` object, and their previous values are listed at the top level of the `ModifiedNode` object rather than in the nested `PreviousFields` object.

### delivered\_amount

The `Amount` of a \[Payment transaction]\[] indicates the amount to deliver to the `Destination`, so if the transaction was successful, then the destination received that much -- **except if the transaction was a partial payment**. (In that case, any positive amount up to `Amount` might have arrived.) Rather than choosing whether or not to trust the `Amount` field, you should use the `delivered_amount` field of the metadata to see how much actually reached its destination.

The `rippled` server provides a `delivered_amount` field in JSON transaction metadata for all successful Payment transactions. This field is formatted like a normal currency amount. However, the delivered amount is not available for transactions that meet both of the following criteria:

* Is a partial payment

If the tx is a partial payment, then `delivered_amount` contains the string value `unavailable` instead of an actual amount. If this happens, you can only figure out the actual delivered amount by reading the `AffectedNodes` in the transaction's metadata.

**Note:** The `delivered_amount` field is generated on-demand for the request, and is not included in the binary format for transaction metadata, nor is it used when calculating the hash of the transaction metadata.

See also: Partial Payments
