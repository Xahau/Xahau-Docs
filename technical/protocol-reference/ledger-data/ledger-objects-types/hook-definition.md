# Hook Definition

[\[Source\]](https://github.com/ripple/rippled/blob/master/src/ripple/protocol/impl/LedgerFormats.cpp#L157-L170)

_(Added by the \[Hooks amendment]\[].)_

A `HookDefinition` object describes a hook, which is a piece of code that is executed in response to certain transactions. The hook can modify the transaction, emit new transactions, or perform other actions.

### Example JSON

```json
{
  "HookHash": "49647F0D748DC3FE26BDACBC57F251AADEFFF391403EC9BF87C97F67E9977FB0",
  "HookOn": "0000000000000000000000000000000000000000000000000000000000000000",
  "HookNamespace": "0000000000000000000000000000000000000000000000000000000000000000",
  "HookParameters": {
    "HookParameter": {
      "HookParameterName": "DEADBEEF",
      "HookParameterValue": "DEADBEEF",
    }
  },
  "HookApiVersion": 1,
  "CreateCode": "5463C6E08862A1FAE5EDAC12D70ADB16546A1F674930521295BC082494B62924",
  "HookSetTxnID": "0000000000000000",
  "ReferenceCount": "6",
  "Fee": "100000000",
  "HookCallbackFee": "200000000",
  "LedgerEntryType": "HookDefinition",
  "index": "49647F0D748DC3FE26BDACBC57F251AADEFFF391403EC9BF87C97F67E9977FB0"
}
```

### Fields

A `HookDefinition` object has the following fields:

| Field             | JSON Type | \[Internal Type]\[] | Required? | Description                                                                                                       |
| ----------------- | --------- | ------------------- | --------- | ----------------------------------------------------------------------------------------------------------------- |
| `HookHash`        | String    | Hash256             | Yes       | The unique identifier of the hook.                                                                                |
| `HookOn`          | String    | Hash256             | Yes       | The account that the hook is attached to.                                                                         |
| `HookNamespace`   | String    | Hash256             | Yes       | The namespace of the hook.                                                                                        |
| `HookParameters`  | String    | Vector              | Yes       | The parameters that the hook accepts.                                                                             |
| `HookApiVersion`  | Number    | UInt16              | Yes       | The version of the hook API that the hook uses.                                                                   |
| `CreateCode`      | String    | VL                  | Yes       | The code that is executed when the hook is created.                                                               |
| `HookSetTxnID`    | String    | Hash256             | Yes       | The ID of the transaction that set the hook.                                                                      |
| `ReferenceCount`  | String    | UInt64              | Yes       | The number of references to the hook.                                                                             |
| `Fee`             | String    | Amount              | Yes       | The fee for executing the hook.                                                                                   |
| `HookCallbackFee` | String    | Amount              | No        | The fee for executing the hook's callback function.                                                               |
| `LedgerEntryType` | String    | UInt16              | Yes       | The value `0x0043`, mapped to the string `HookDefinition`, indicates that this object is a HookDefinition object. |

#### Hook Definition ID Format

The ID of a `HookDefinition` object is the \[SHA-512Half]\[] of the following values, concatenated in order:

* The HookDefinition space key (`0x0044`)
* The `HookHash` of the hook
