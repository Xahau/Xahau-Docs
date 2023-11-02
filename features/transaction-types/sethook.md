---
description: >-
  The SetHook transaction allows users to install, update, delete, or perform
  other operations on hooks in the XRP Ledger.
---

# SetHook

\[[Source](https://github.com/Xahau/xahaud/blob/dev/src/ripple/app/tx/impl/SetHook.cpp)]

_(Added by the \[Hooks amendment]\[].)_

### Example

<pre class="language-json"><code class="lang-json">{
    "TransactionType": "SetHook",
    "Account": "rWYkbWkCeg8dP6rXALnjgZSjjLyih5NXm",
    "Flags": 0,
    "Hooks": [
<strong>        {
</strong>            "HookHash": "610F33B8EBF7EC795F822A454FB852156AEFE50BE0CB8326338A81CD74801864",
            "CreateCode": "697066733A2F2F4445414442454546697066733A2F2F44454144424545467878",
            "HookGrants": [],
            "HookNamespace": "0000000000000000000000000000000000000000000000000000000000000000",
            "HookParameters": [],
            "HookOn": "0000000000000000000000000000000000000000000000000000000000000000",
            "HookApiVersion": 0,
            "Flags": 0
        }
    ]
}
</code></pre>

| Field     | JSON Type | \[Internal Type]\[] | Description                                        |
| --------- | --------- | ------------------- | -------------------------------------------------- |
| `Account` | String    | AccountID           | The address of the account that will own the hook. |
| `Hooks`   | Array     | Array               | The array of hooks to be set.                      |

### Special Transaction Cost

The SetHook transaction has a standard transaction cost, which is the minimum transaction cost required for all transactions.

### Error Cases

Besides errors that can occur for all transactions, SetHook transactions can result in the following transaction result codes:

| Error Code      | Description                                                                  |
| --------------- | ---------------------------------------------------------------------------- |
| `tecDUPLICATE`  | Occurs if a hook with the same hash already exists.                          |
| `tecDIR_FULL`   | Occurs if the owner's directory is full and cannot accommodate the new hook. |
| `terNO_ACCOUNT` | Occurs if the sending account does not exist.                                |
| `terNO_HOOK`    | Occurs if no hook exists with the specified hash.                            |
| `temDISABLED`   | Occurs if the Hooks Amendment is not enabled.                                |
| `temMALFORMED`  | Occurs if the transaction is malformed.                                      |

### SetHook Operations

The SetHook transaction supports the following operations:

**Install**

To install a new hook, include the `HookHash`, `CreateCode`, `HookGrants`, `HookNamespace`, `HookParameters`, `HookOn`, `HookApiVersion`, and `Flags` fields in the hook object. The `HookHash` field specifies the hash of the hook, the `CreateCode` field contains the WebAssembly code for the hook, the `HookGrants` field specifies the grants associated with the hook, the `HookNamespace` field specifies the namespace of the hook, the `HookParameters` field contains the parameters of the hook, the `HookOn` field specifies the event on which the hook is triggered, the `HookApiVersion` field specifies the API version of the hook, and the `Flags` field specifies additional flags for the hook.

**Update**

To update an existing hook, include the `HookHash`, `HookGrants`, `HookNamespace`, `HookParameters`, `HookOn`, `Flags` fields in the hook object. The `HookHash` field specifies the hash of the hook, the `HookGrants` field specifies the grants associated with the hook, the `HookNamespace` field specifies the namespace of the hook, the `HookParameters` field contains the parameters of the hook, the `HookOn` field specifies the event on which the hook is triggered, and the `Flags` field specifies additional flags for the hook.

**Delete**

To delete an existing hook, include the `HookHash` field in the hook object. The `HookHash` field specifies the hash of the hook to be deleted.

**Namespace Delete**

To delete an entire namespace of hooks, include the `HookNamespace` field and set the `Flags` field to `hsfNSDELETE` in the hook object. The `HookNamespace` field specifies the namespace to be deleted.

**No-op**

To perform a no-op operation, include an empty hook object in the `Hooks` array. This can be useful to group multiple SetHook operations in a single transaction.

### Hook Fields

The following fields are used in the hook object:

| Field            | JSON Type | Internal Type | Description                               |
| ---------------- | --------- | ------------- | ----------------------------------------- |
| `HookHash`       | String    | Hash256       | The hash of the hook.                     |
| `CreateCode`     | String    | Blob          | The WebAssembly code for the hook.        |
| `HookGrants`     | Array     | Array         | The grants associated with the hook.      |
| `HookNamespace`  | String    | Hash256       | The namespace of the hook.                |
| `HookParameters` | Array     | Array         | The parameters of the hook.               |
| `HookOn`         | String    | Hash256       | The event on which the hook is triggered. |
| `HookApiVersion` | Number    | UInt16        | The API version of the hook.              |
| `Flags`          | Number    | UInt32        | Additional flags for the hook.            |

### Flags

The `Flags` field in the hook object specifies additional flags for the hook. The following flags are supported:

| Flag Name     | Description                                                              |
| ------------- | ------------------------------------------------------------------------ |
| `hsfOVERRIDE` | Allows the hook to be deleted even if it is referenced by other objects. |
| `hsfNSDELETE` | Deletes an entire namespace of hooks.                                    |
| `hsfCOLLECT`  | Collects the hook's associated objects.                                  |

### Hook Grants

The `HookGrants` field is an array of objects that specify the grants associated with the hook. Each grant object has the following fields:

| Field       | JSON Type | Internal Type | Description                                        |
| ----------- | --------- | ------------- | -------------------------------------------------- |
| `HookHash`  | String    | Hash256       | The hook to apply the grant to.                    |
| `Authorize` | String    | AccountID     | The address of the account that is granted access. |
| `Flags`     | Number    | Uint32        | Flags                                              |

### Hook Parameters

The `HookParameters` field is an array of objects that specify the parameters of the hook. Each parameter object has the following fields:

| Field   | JSON Type | Internal Type | Description                 |
| ------- | --------- | ------------- | --------------------------- |
| `Name`  | String    | Blob          | The name of the parameter.  |
| `Value` | String    | Blob          | The value of the parameter. |

### Hook Executions

When Hooks execute they leave behind information about the status of that execution. This appears in the Originating Transaction metadata as an `sfHookExecutions` block. This block contains the following fields:

| Field                  | JSON Type | Internal Type | Description                                                                                                                                                  |
| ---------------------- | --------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `HookAccount`          | String    | AccountID     | The account the Hook ran on.                                                                                                                                 |
| `HookEmitCount`        | Number    | UInt16        | The total number of Emitted Transactions produced by the Hook.                                                                                               |
| `HookExecutionIndex`   | Number    | UInt16        | The SHA512H of the Hook at the time it was executed.                                                                                                         |
| `HookHash`             | String    | Hash256       | The value of the parameter.                                                                                                                                  |
| `HookInstructionCount` | String    | UInt64        | The total number of webassembly instructions that were executed when the Hook ran.                                                                           |
| `HookResult`           | Number    | UInt8         | <p>Hooks can end in three ways: <code>accept</code>, <code>rollback</code> and <code>error</code>.<br>This is <em>not</em> the same as sfHookReturnCode!</p> |
| `HookReturnCode`       | String    | UInt64        | The integer returned as the third parameter of `accept` or `rollback`.                                                                                       |
| `HookReturnString`     | String    | Blob          | The string returned in the first two parameters of `accept` or `rollback`, if any.                                                                           |
| `HookStateChangeCount` | Number    | UInt16        | The number of Hook State changes the Hook made during execution.                                                                                             |

