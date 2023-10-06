# Hook State

[\[Source\]](https://github.com/ripple/rippled/blob/master/src/ripple/protocol/impl/LedgerFormats.cpp#L157-L170)

_(Added by the \[Hooks amendment]\[].)_

A `HookState` object describes the state of a hook, which is a piece of code running on the XRP Ledger that can interact with transactions. The `HookState` object stores the state of the hook, which can be modified by the hook's code.

### Example JSON

```json
{
  "OwnerNode": "0000000000000000",
  "HookStateKey": "49647F0D748DC3FE26BDACBC57F251AADEFFF391403EC9BF87C97F67E9977FB0",
  "HookStateData": "46060241FABCF692D4D934BA2A6C4427CD4279083E38C77CBE642243E43BE291",
  "LedgerEntryType": "HookState",
  "index": "5463C6E08862A1FAE5EDAC12D70ADB16546A1F674930521295BC082494B62924"
}
```

### Fields

A `HookState` object has the following fields:

| Field             | JSON Type | \[Internal Type]\[] | Required? | Description                                                                                                                   |
| ----------------- | --------- | ------------------- | --------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `OwnerNode`       | String    | UInt64              | Yes       | A hint indicating which page of the owner's directory links to this object, in case the directory consists of multiple pages. |
| `HookStateKey`    | String    | Hash256             | Yes       | The key that uniquely identifies this hook state.                                                                             |
| `HookStateData`   | String    | VL                  | Yes       | The data stored by the hook. This can be any data that the hook's code decides to store.                                      |
| `LedgerEntryType` | String    | UInt16              | Yes       | The value `0x0043`, mapped to the string `HookState`, indicates that this object is a HookState object.                       |

#### HookState ID Format

[\[Source\]](https://github.com/ripple/rippled/blob/master/src/ripple/protocol/impl/Indexes.cpp#L193-L200)

The ID of a `HookState` object is the \[SHA-512Half]\[] of the following values, concatenated in order:

* The HookState space key (`0x0076`)
* The AccountID of the account that owns the hook
* The `HookStateKey` of the `HookState` object
