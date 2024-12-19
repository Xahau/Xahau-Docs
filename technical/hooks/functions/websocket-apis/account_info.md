# account\_info

### New features

The `account_info` API will now provide, in addition to its regular behaviour:

* A list of namespaces currently in use by at least one Hook State Object
* A total count of all Hook State Objects the account has

Example query:

JSON

```json
{
  "command": "account_info",
  "account": "raaFre81618XegCrzTzVotAmarBcqNSAvK"
}
```

E.g.

JSON

```json
{
  "result": {
    "account_data": {
      "Account": "raaFre81618XegCrzTzVotAmarBcqNSAvK",
      ...,
      "HookNamespaces": [
        "01EAF09326B4911554384121FF56FA8FECC215FDDE2EC35D9E59F2C53EC665A0"
      ],
      "HookStateCount": 49,
      ...
    },
    "ledger_current_index": 5555046,
    "validated": false
  },
  "status": "success",
  "type": "response"
}
```
