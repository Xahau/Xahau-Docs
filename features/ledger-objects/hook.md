# Hook

[\[Source\]](https://github.com/ripple/rippled/blob/master/src/ripple/protocol/impl/LedgerFormats.cpp#L157-L170)

_(Added by the \[Hooks amendment]\[].)_

A `Hook` object describes a smart contract, which can be triggered by a transaction to perform predefined operations. The operations are defined by the `Hook` creator and can interact with the ledger and transactions.

### Example JSON

```json
{
  "Account": "rUn84CUYbNjRoTQ6mSW7BVJPSVJNLb1QLo",
  "OwnerNode": "0000000000000000",
  "PreviousTxnID": "5463C6E08862A1FAE5EDAC12D70ADB16546A1F674930521295BC082494B62924",
  "PreviousTxnLgrSeq": 6,
  "Hooks": [
    {
      "HookHash": "46060241FABCF692D4D934BA2A6C4427CD4279083E38C77CBE642243E43BE291",
      "CreateCode": "100000000",
      "HookGrants": [],
      "HookNamespace": "myHook",
      "HookParameters": [],
      "HookOn": "5463C6E08862A1FAE5EDAC12D70ADB16546A1F674930521295BC082494B62924",
      "HookApiVersion": 1,
      "Flags": 0
    }
  ],
  "LedgerEntryType": "Hook",
  "index": "49647F0D748DC3FE26BDACBC57F251AADEFFF391403EC9BF87C97F67E9977FB0"
}
```

### Fields

A `Hook` object has the following fields:

| Field               | JSON Type | \[Internal Type]\[] | Required? | Description                                                                                                                                                                     |
| ------------------- | --------- | ------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Account`           | String    | Account             | Yes       | The account that created the Hook.                                                                                                                                              |
| `OwnerNode`         | String    | UInt64              | Yes       | A hint indicating which page of the owner's directory links to this object, in case the directory consists of multiple pages.                                                   |
| `PreviousTxnID`     | String    | Hash256             | Yes       | The ID of the transaction that most recently modified this object.                                                                                                              |
| `PreviousTxnLgrSeq` | Number    | UInt32              | Yes       | The \[ledger index]\[] of the ledger that contains the transaction that most recently modified this object.                                                                     |
| `Hooks`             | Array     | Array               | Yes       | An array of hook objects. Each object has the following fields: `HookHash`, `CreateCode`, `HookGrants`, `HookNamespace`, `HookParameters`, `HookOn`, `HookApiVersion`, `Flags`. |
| `LedgerEntryType`   | String    | UInt16              | Yes       | The value `0x0043`, mapped to the string `Hook`, indicates that this object is a Hook object.                                                                                   |

#### Hook ID Format

The ID of a `Hook` object is the \[SHA-512Half]\[] of the following values, concatenated in order:

* The Hook space key (`0x0048`)
* The AccountID of the sender of the \[SetHook transaction]\[] that created the `Hook` object
* The `Sequence` number of the \[SetHook transaction]\[] that created the `Hook` object. If the HookCreate transaction used a Ticket, use the `TicketSequence` value instead.
