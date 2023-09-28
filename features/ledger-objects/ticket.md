# Ticket

[\[Source\]](https://github.com/ripple/rippled/blob/76a6956138c4ecd156c5c408f136ed3d6ab7d0c1/src/ripple/protocol/impl/LedgerFormats.cpp#L155-L164)

_(Added by the \[TicketBatch amendment]\[].)_

The `Ticket` object type represents a Ticket, which tracks an account \[sequence number]\[Sequence Number] that has been set aside for future use. You can create new tickets with a \[TicketCreate transaction]\[]. \[New in: rippled 1.7.0]\[]

### Example JSON

```json
{
  "Account": "rEhxGqkqPPSxQ3P25J66ft5TwpzV14k2de",
  "Flags": 0,
  "LedgerEntryType": "Ticket",
  "OwnerNode": "0000000000000000",
  "PreviousTxnID": "F19AD4577212D3BEACA0F75FE1BA1644F2E854D46E8D62E9C95D18E9708CBFB1",
  "PreviousTxnLgrSeq": 4,
  "TicketSequence": 3
}
```

### Fields

A `Ticket` object has the following fields:

<table><thead><tr><th>Name</th><th width="139">JSON Type</th><th width="137">Internal Type</th><th width="115">Required?</th><th>Description</th></tr></thead><tbody><tr><td><code>Account</code></td><td>String</td><td>AccountID</td><td>Yes</td><td>The account that owns this Ticket.</td></tr><tr><td><code>Flags</code></td><td>Number</td><td>UInt32</td><td>Yes</td><td>A bit-map of boolean flags enabled for this object. Currently, the protocol defines no flags for <code>Ticket</code> objects. The value is always <code>0</code>.</td></tr><tr><td><code>LedgerEntryType</code></td><td>String</td><td>UInt16</td><td>Yes</td><td>The value <code>0x0054</code>, mapped to the string <code>Ticket</code>, indicates that this object is a {{currentpage.name}} object.</td></tr><tr><td><code>OwnerNode</code></td><td>String</td><td>UInt64</td><td>Yes</td><td>A hint indicating which page of the owner directory links to this object, in case the directory consists of multiple pages. <strong>Note:</strong> The object does not contain a direct link to the owner directory containing it, since that value can be derived from the <code>Account</code>.</td></tr><tr><td><code>PreviousTxnID</code></td><td>String</td><td>Hash256</td><td>Yes</td><td>The identifying hash of the transaction that most recently modified this object.</td></tr><tr><td><code>PreviousTxnLgrSeq</code></td><td>Number</td><td>UInt32</td><td>Yes</td><td>The [index of the ledger][Ledger Index] that contains the transaction that most recently modified this object.</td></tr><tr><td><code>TicketSequence</code></td><td>Number</td><td>UInt32</td><td>Yes</td><td>The [Sequence Number][] this Ticket sets aside.</td></tr></tbody></table>

### Ticket ID Format

The ID of a Ticket object is the SHA-512Half of the following values, concatenated in order:

* The Ticket space key (`0x0054`)
* The AccountID of the owner of the Ticket
* The `TicketSequence` number of the Ticket
