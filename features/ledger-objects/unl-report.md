# UNL Report

_(Added by the \[Hooks amendment]\[].)_

A `UNLReport` object describes a report of the Unique Node List (UNL) which is a list of validator nodes that are trusted by the network to validate transactions.

### Example JSON

```json
{
  "LedgerEntryType": "UNLReport",
  "PreviousTxnID": "5463C6E08862A1FAE5EDAC12D70ADB16546A1F674930521295BC082494B62924",
  "PreviousTxnLgrSeq": 6,
  "ImportVLKeys": [
    {
      "PublicKey": "n9LigbVAi4pQc6pU2KJvQZV5wqJ8C3sVvZvBZUopchH8vqa6PEKy",
      "Account": "rUn84CUYbNjRoTQ6mSW7BVJPSVJNLb1QLo"
    }
  ],
  "ActiveValidators": [
    {
      "PublicKey": "n9LigbVAi4pQc6pU2KJvQZV5wqJ8C3sVvZvBZUopchH8vqa6PEKy",
      "Account": "rUn84CUYbNjRoTQ6mSW7BVJPSVJNLb1QLo"
    }
  ],
  "index": "49647F0D748DC3FE26BDACBC57F251AADEFFF391403EC9BF87C97F67E9977FB0"
}
```

### Fields

A `UNLReport` object has the following fields:

| Field               | JSON Type | \[Internal Type]\[] | Required? | Description                                                                                                                                         |
| ------------------- | --------- | ------------------- | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| `LedgerEntryType`   | String    | UInt16              | Yes       | The value `0x0073`, mapped to the string `UNLReport`, indicates that this object is a UNLReport object.                                             |
| `PreviousTxnID`     | String    | Hash256             | Yes       | The identifying hash of the transaction that most recently modified this object.                                                                    |
| `PreviousTxnLgrSeq` | Number    | UInt32              | Yes       | The index of the ledger that contains the transaction that most recently modified this object.                                                      |
| `ImportVLKeys`      | Array     | Array               | No        | An array of objects, each representing a validator key that has been imported. Each object has a `PublicKey` field and an optional `Account` field. |
| `ActiveValidators`  | Array     | Array               | No        | An array of objects, each representing an active validator. Each object has a `PublicKey` field and an optional `Account` field.                    |

### ImportVLKey

| Field       | JSON Type | \[Internal Type]\[] | Required? | Description                                                                     |
| ----------- | --------- | ------------------- | --------- | ------------------------------------------------------------------------------- |
| `PublicKey` | String    | VL                  | Yes       | The public key of the imported validator.                                       |
| `Account`   | String    | Account             | No        | The account associated with the imported validator key. This field is optional. |

### ActiveValidator

| Field       | JSON Type | \[Internal Type]\[] | Required? | Description                                                               |
| ----------- | --------- | ------------------- | --------- | ------------------------------------------------------------------------- |
| `PublicKey` | String    | VL                  | Yes       | The public key of the active validator.                                   |
| `Account`   | String    | Account             | No        | The account associated with the active validator. This field is optional. |
