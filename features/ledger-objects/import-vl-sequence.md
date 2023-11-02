# Import VL Sequence

_(Added by the \[Import amendment]\[].)_

A `ImportVLSequence` object describes a report of the Unique Node List (UNL) which is a list of validator nodes that are trusted by the network to validate transactions.

### Example JSON

```json
{
  "LedgerEntryType": "ImportVLSequence",
  "Flags": 0,
  "ImportSequence": 2023102101,
  "PublicKey": "n9LigbVAi4pQc6pU2KJvQZV5wqJ8C3sVvZvBZUopchH8vqa6PEKy",
  "index": "49647F0D748DC3FE26BDACBC57F251AADEFFF391403EC9BF87C97F67E9977FB0"
}
```

### Fields

A `UNLReport` object has the following fields:

| Field             | JSON Type | \[Internal Type]\[] | Required? | Description                                                                                                           |
| ----------------- | --------- | ------------------- | --------- | --------------------------------------------------------------------------------------------------------------------- |
| `LedgerEntryType` | String    | UInt16              | Yes       | The value `0x0049`, mapped to the string `UNLReport`, indicates that this object is a UNLReport object.               |
| `Flags`           | Number    | UInt32              | Yes       | A bit-map of boolean flags. No flags are defined for the `ImportVLSequence` object type, so this value is always `0`. |
| `ImportSequence`  | Number    | UInt32              | Yes       |                                                                                                                       |
| `PublicKey`       | String    | Blob                | Yes       |                                                                                                                       |

#### Import VL Sequence ID Format

The ID of a `ImportVLSequence` object is the \[SHA-512Half]\[] of the following values, concatenated in order:

* The Import VL Sequence space key (`0x0049`)
* The Public Key of the Import Validator List
