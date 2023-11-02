# Ledger Objects

## Ledger Header

[\[Source\]](https://github.com/ripple/rippled/blob/master/src/ripple/ledger/ReadView.h#L71)

Every ledger version has a unique header that describes the contents. You can look up a ledger's header information with the \[ledger method]\[]. The contents of the ledger header are as follows:

<table><thead><tr><th>Field</th><th width="145">JSON Type</th><th width="153">[Internal Type][]</th><th>Description</th></tr></thead><tbody><tr><td><code>ledger_index</code></td><td>String</td><td>UInt32</td><td>The [ledger index][Ledger Index] of the ledger. Some API methods display this as a quoted integer; some display it as a native JSON number.</td></tr><tr><td><code>ledger_hash</code></td><td>String</td><td>Hash256</td><td>The [SHA-512Half][] of this ledger version. This serves as a unique identifier for this ledger and all its contents.</td></tr><tr><td><code>account_hash</code></td><td>String</td><td>Hash256</td><td>The [SHA-512Half][] of this ledger's state tree information.</td></tr><tr><td><code>close_time</code></td><td>Number</td><td>UInt32</td><td>The approximate time this ledger version closed, as the number of seconds since the Ripple Epoch of 2000-01-01 00:00:00. This value is rounded based on the <code>close_time_resolution</code>.</td></tr><tr><td><code>closed</code></td><td>Boolean</td><td>Boolean</td><td>If <code>true</code>, this ledger version is no longer accepting new transactions. (However, unless this ledger version is validated, it might be replaced by a different ledger version with a different set of transactions.)</td></tr><tr><td><code>parent_hash</code></td><td>String</td><td>Hash256</td><td>The <code>ledger_hash</code> value of the previous ledger version that is the direct predecessor of this one. If there are different versions of the previous ledger index, this indicates from which one the ledger was derived.</td></tr><tr><td><code>total_coins</code></td><td>String</td><td>UInt64</td><td>The total number of [drops of XRP][] owned by accounts in the ledger. This omits XRP that has been destroyed by transaction fees. The actual amount of XRP in circulation is lower because some accounts are "black holes" whose keys are not known by anyone.</td></tr><tr><td><code>transaction_hash</code></td><td>String</td><td>Hash256</td><td>The [SHA-512Half][] of the transactions included in this ledger.</td></tr><tr><td><code>close_time_resolution</code></td><td>Number</td><td>Uint8</td><td>An integer in the range [2,120] indicating the maximum number of seconds by which the <code>close_time</code> could be rounded.</td></tr><tr><td><code>closeFlags</code></td><td>(Omitted)</td><td>UInt8</td><td>A bit-map of flags relating to the closing of this ledger.</td></tr></tbody></table>

### Ledger Index

### Close Flags

The ledger has only one flag defined for `closeFlags`: **`sLCF_NoConsensusTime`** (value `1`). If this flag is enabled, it means that validators had different close times for the ledger but built otherwise the same ledger, so they declared consensus while "agreeing to disagree" on the close time.&#x20;

In this case, the official `close_time` value of the ledger is 1 second after that of the parent ledger.

The `closeFlags` field is not included in any JSON representations of a ledger but is included in the binary representation of a ledger and is one of the fields that determine the ledger's hash.
