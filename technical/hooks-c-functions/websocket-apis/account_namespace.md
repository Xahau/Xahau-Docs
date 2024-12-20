# account\_namespace

Use the `account_namespace` websocket API to query the Hook State Objects on a particular account in a particular namespace.

Usage:

JSON

```json
{
  "command": "account_namespace",
  "account": "<r Address>",
  "namespace_id": "<Namespace HEX>"
}
```

Example query:

JSON

```json
{
  "command": "account_namespace",
  "account": "raaFre81618XegCrzTzVotAmarBcqNSAvK",
  "namespace_id": "01EAF09326B4911554384121FF56FA8FECC215FDDE2EC35D9E59F2C53EC665A0"
}
```

Example result:

JSON

```json
{
  "result": {
    "account": "raaFre81618XegCrzTzVotAmarBcqNSAvK",
    "ledger_current_index": 5554739,
    "namespace_entries": [
      {
        "Flags": 0,
        "HookStateData": "CE66D3EBD1A91E9D6F47ADCF8890C92C3EE65A42313174682047656E20496E74656C28522920436F726528544D292069372D31313635473720322E3800080AF0000C3500000009C400000FA0",
        "HookStateKey": "4556520237F1F3A48DFAED331FDB8F894522B5CE634C86A0258BA1B300000018",
        "LedgerEntryType": "HookState",
        "OwnerNode": "0",
        "index": "065E103AC0838155A392DECA99D77FAE768EC822BFEC6BC999268ECBD16C8FAF"
      },
      {
        "Flags": 0,
        "HookStateData": "00000000044E8000",
        "HookStateKey": "4556520100000000000000000000000000000000000000000000000000000004",
        "LedgerEntryType": "HookState",
        "OwnerNode": "0",
        "index": "0890BE9EE8CD129D21728FC3C2423CC0AB99D325A269A8A749C840F712989E5B"
      },
      ... 
    ],
    "namespace_id": "01EAF09326B4911554384121FF56FA8FECC215FDDE2EC35D9E59F2C53EC665A0",
    "validated": false
  },
  "status": "success",
  "type": "response"
}
```
