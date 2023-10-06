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

| Name                | JSON Type | Internal Type | Required? | Description                                                                                                                                                                                                                                                               |
| ------------------- | --------- | ------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Account`           | String    | AccountID     | Yes       | The account that owns this Ticket.                                                                                                                                                                                                                                        |
| `Flags`             | Number    | UInt32        | Yes       | A bit-map of boolean flags enabled for this object. Currently, the protocol defines no flags for `Ticket` objects. The value is always `0`.                                                                                                                               |
| `LedgerEntryType`   | String    | UInt16        | Yes       | The value `0x0054`, mapped to the string `Ticket`, indicates that this object is a \{{currentpage.name\}} object.                                                                                                                                                         |
| `OwnerNode`         | String    | UInt64        | Yes       | A hint indicating which page of the owner directory links to this object, in case the directory consists of multiple pages. **Note:** The object does not contain a direct link to the owner directory containing it, since that value can be derived from the `Account`. |
| `PreviousTxnID`     | String    | Hash256       | Yes       | The identifying hash of the transaction that most recently modified this object.                                                                                                                                                                                          |
| `PreviousTxnLgrSeq` | Number    | UInt32        | Yes       | The \[index of the ledger]\[Ledger Index] that contains the transaction that most recently modified this object.                                                                                                                                                          |
| `TicketSequence`    | Number    | UInt32        | Yes       | The \[Sequence Number]\[] this Ticket sets aside.                                                                                                                                                                                                                         |

### Ticket ID Format

The ID of a Ticket object is the SHA-512Half of the following values, concatenated in order:

* The Ticket space key (`0x0054`)
* The AccountID of the owner of the Ticket
* The `TicketSequence` number of the Ticket
