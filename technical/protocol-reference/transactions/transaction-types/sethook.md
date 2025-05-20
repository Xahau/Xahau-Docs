---
description: >-
  The SetHook transaction allows users to install, update, delete, or perform
  other operations on hooks in Xahau.
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
</strong><strong>            "Hook": {
</strong><strong>                "HookHash": "610F33B8EBF7EC795F822A454FB852156AEFE50BE0CB8326338A81CD74801864",
</strong>                "CreateCode": "697066733A2F2F4445414442454546697066733A2F2F44454144424545467878",
                "HookGrants": [],
                "HookNamespace": "0000000000000000000000000000000000000000000000000000000000000000",
                "HookParameters": [],
                "HookOn": "0000000000000000000000000000000000000000000000000000000000000000",
                "HookApiVersion": 0,
                "Flags": 0
<strong>            }
</strong>        }
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

There are six possible operations: No Operation, Create, Update, Delete, Install and Namespace Delete

Each operation is specified by the inclusion or omission of certain HookSet Object fields. This might seem confusing at first but by working through a few examples the reader should find it intuitive; Essentially HookSet operations are a type of **diff** between a specific Hook's _defaults_, _existing_ and newly specified fields.

Achieving each type of operation is explained in a subsection below.

### No Operation

**Occurs when**:

* The HookSet Object is empty

**Behaviour**:

* No change of any kind is made.

**Example**:

JSON

```json
{ 
    Account: "r4GDFMLGJUKMjNhhycgt2d5LXCdXzCYPoc",
    TransactionType: "SetHook",
    Fee: "2000000",
    Hooks:
    [        
        {                        
            Hook: {}
        }
    ]
}
```

### Create Operation

**Occurs when**:

_All_ of the following conditions are met:

* The Corresponding Hook does not exist _or_`FLAG_OVERRIDE` is specified.
* `CreateCode` field is specified and is not blank and contains the valid web assembly bytecode for a valid Hook.
* No instance of the same web assembly bytecode already exists on the XRPL. (If it does and all other requirements are met then interpret as an Install Operation — see below.)

**Behaviour**:

* A reference counted `HookDefinition` object is created on the XRPL containing the fields in the HookSet Object, with all specified fields (Namespace, Parameters, HookOn) becoming defaults (but not Grants.)
* A `Hooks` array is created on the executing account, if it doesn't already exist. (This is the structure that contains the Corresponding Hooks.)
* A `Hook` object is created at the Corresponding Hook position if one does not already exist.
* The `Hook` object points at the `HookDefinition`.
* The `Hook` object contains no fields except `HookHash` which points at the created `HookDefinition`.
* If `hsfNSDELETE` flag is specified then any HookState entires in the destination namespace are deleted if they currently exist.

**Example**:

JSON

```json
{ 
    Account: "r4GDFMLGJUKMjNhhycgt2d5LXCdXzCYPoc",
    TransactionType: "SetHook",
    Fee: "2000000",
    Hooks:
    [        
        {                        
            Hook: {                
                CreateCode: fs.readFileSync('accept.wasm').toString('hex').toUpperCase(),
                HookOn: '0000000000000000',
                HookNamespace: addr.codec.sha256('accept').toString('hex').toUpperCase(),
                HookApiVersion: 0
            }
        }
    ]
}
```

### Install Operation

**Occurs when**:

_All_ of the following conditions are met:

* The Corresponding Hook does not exist _or_`FLAG_OVERRIDE` is specified.
* `HookHash` field is specified and is not blank and contains the hash of a Hook that already exists as a `HookDefinition` on the ledger _or_ `CreateCode` field is specified and is not blank and contains the valid web assembly bytecode for a valid hook that already exists on the ledger as a `HookDefinition`.

**Behaviour**:

* The reference count of the `HookDefinition` object is incremented.
* A `Hooks` array is created on the executing account, if it doesn't already exist. (This is the structure that contains the Corresponding Hooks.)
* A `Hook` object is created at the Corresponding Hook position if one does not already exist.
* The `Hook` object points at the `HookDefinition`.
* The `Hook` object contains all the fields in the HookSet Object, except and unless:
* A field or key-pair within a field is identical to the Hook Defaults set on the `HookDefinition`, in which case it is omitted due to defaults.
* If `hsfNSDELETE` flag is specified then any HookState entires in the destination namespace are deleted if they currently exist.

**Example**:

JSON

```json
{ 
    Account: "r4GDFMLGJUKMjNhhycgt2d5LXCdXzCYPoc",
    TransactionType: "SetHook",
    Fee: "2000000",
    Hooks:
    [        
        {                        
            Hook: {                
                HookHash: "A5663784D04ED1B4408C6B97193464D27C9C3334AAF8BBB4FA5EB8E557FC4A2C",
                HookOn: '0000000000000000',
                HookNamespace: addr.codec.sha256('accept').toString('hex').toUpperCase(),
            }
        }
    ]
}
```

### Update Operation

**Occurs when**:

_All_ of the following conditions are met:

* The Corresponding Hook exists.
* `HookHash` is absent.
* `CreateCode` is absent.
* One or more of `HookNamespace`, `HookParameters` or `HookGrants` is present.

**General Behaviour**:

* The Corresponding Hook is updated in such a way that the desired changes are reflected in the Corresponding Hook.

**Specific Behaviour**:

If `HookNamespace` is specified and differs from the Corresponding Hook's Namespace:

* the Corresponding Hook's `HookNamespace` is updated, and
* if the `hsfNSDELETE` flag is specified all HookState entires in the old namespace are deleted.

If `HookParameters` is specified, then for each entry:

* If `HookParameterName` exists but `HookParameterValue` is absent and the Corresponding Hook's Parameters (either specifically or via defaults) contains this `HookParameterName` then the parameter is marked as deleted on the Corresponding Hook.
* If `HookParameterName` exists and `HookParameterValue` exists then the Corresponding Hook's Parameters are modified to include the new or updated parameter.

If `HookGrants` is specified then:

* The Corresponding Hook's `HookGrants` array is replaced with the array.

**Example**:

JSON

```json
{ 
    Account: "r4GDFMLGJUKMjNhhycgt2d5LXCdXzCYPoc",
    TransactionType: "SetHook",
    Fee: "2000000",
    Hooks:
    [        
        {                        
            Hook: {
                HookNamespace: addr.codec.sha256('new_accept').toString('hex').toUpperCase(),
            }
        }
    ]
}
```

### Delete Operation

**Occurs when**:

_All_ of the following conditions are met:

* The Corresponding Hook exists.
* `hsfOVERRIDE` is specified.
* optionally `hsfNSDELETE` is also specified.
* `HookHash` is absent.
* `CreateCode` is present but empty.

**Behaviour**:

* The reference count of the `HookDefinition` object is decremented.
* If the reference count is now zero the `HookDefintion` is removed from the ledger.
* The `Hook` object in the Corresponding Hook position is deleted, leaving an empty position.
* If `hsfNSDELETE` is specified the namespace and all HookState entries are also deleted.

**Example**:

JSON

```json
{ 
    Account: "r4GDFMLGJUKMjNhhycgt2d5LXCdXzCYPoc",
    TransactionType: "SetHook",
    Fee: "2000000",
    Hooks:
    [        
        {                        
            Hook: {
                CreateCode: "",
                Flags: 1,
            }
        }
    ]
}
```

### Namespace Reset

**Occurs when**:

_All_ of the following conditions are met:

* `flags` is present and `hsfNSDELETE` is set. `hsfOVERRIDE` can optionally also be specified if the Hook at this position is to be deleted.
* `HookNamespace` is specified.
* `CreateCode` is absent.
* `HookHash` is absent.
* `HookGrants`, `HookParameters`, `HookOn` and `HookApiVersion` are absent.

**Behaviour**:

* If the Corresponding Hook exists, it remains, nothing happens to it.
* A subset of HookState objects and the HookState directory for the specified namespace are removed from the ledger, up to the defined limit (512). Further transactions are needed to continue the deletion process until all relevant records are removed. See [`tesPARTIAL`](https://docs.xahau.network/technical/protocol-reference/transactions/transaction-results/tes-codes).&#x20;

**Example**:

JSON

```json
{ 
    Account: "r4GDFMLGJUKMjNhhycgt2d5LXCdXzCYPoc",
    TransactionType: "SetHook",
    Fee: "2000000",
    Hooks:
    [        
        {                        
            Hook: {
              	HookNamespace: addr.codec.sha256('accept').toString('hex').toUpperCase(),
                Flags: 3,
            }
        }
    ]
}
```

### Hook Fields

The following fields are used in the hook object:

| Field            | JSON Type | Internal Type | Description                                       |
| ---------------- | --------- | ------------- | ------------------------------------------------- |
| `HookHash`       | String    | Hash256       | The hash of the hook.                             |
| `CreateCode`     | String    | Blob          | The WebAssembly code for the hook.                |
| `HookGrants`     | Array     | Array         | The grants associated with the hook.              |
| `HookNamespace`  | String    | Hash256       | The namespace of the hook.                        |
| `HookParameters` | Array     | Array         | The parameters of the hook.                       |
| `HookOn`         | String    | Hash256       | The transaction/s on which the hook is triggered. |
| `HookCanEmit`    | String    | Hash256       | The transaction/s which the hook can emit.        |
| `HookApiVersion` | Number    | UInt16        | The API version of the hook.                      |
| `Flags`          | Number    | UInt32        | Additional flags for the hook.                    |

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

| Field                | JSON Type | Internal Type | Description                 |
| -------------------- | --------- | ------------- | --------------------------- |
| `HookParameterName`  | String    | Blob          | The name of the parameter.  |
| `HookParameterValue` | String    | Blob          | The value of the parameter. |

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

