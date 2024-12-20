# SetHook Transaction

### SetHook Transaction

Hook web assembly bytecode is installed onto an Xahau account using the `SetHook` transaction.

An example appears below:

```js
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

The transaction is deceptively simple, but hides significant complexity, described below.

### Hooks Array

The main body of the SetHook transaction is the hooks array:

```js
{
    Account: "r4GDFMLGJUKMjNhhycgt2d5LXCdXzCYPoc",
    TransactionType: "SetHook",
    Hooks:                         // This is the Hooks Array
    [            
          {  Hook: { ... }  },     // HookSet Object (position 0)
          {  Hook: { ... }  },  
          {  Hook: { ... }  },  
          {  Hook: { ... }  }.     // HookSet Object (position 3)
    ]
}
```

This array _mirrors_ the [Hook Chain](chaining.md) installed on the account:

* Position 0 in the array _corresponds_ to position 0 in the Hook Chain.
* Position 3 in the array _corresponds_ to position 3 in the Hook Chain, etc.

### HookSet Object and Corresponding Hook

Each entry in the Hooks Array (in the SetHook Transaction) is called a _HookSet Object_, and its corresponding Hook in the account's Hook Chain is called the _Corresponding Hook_.

<figure><img src="../../../.gitbook/assets/spaces_m6f29os4wP16vCS4lHNh_uploads_NbV5W3McCRKkL4eJeF6v_cdf692e-sethook.png" alt=""><figcaption><p>Example: A user performs an operation on each Hook in his/her Hook chain with a SetHook transaction.</p></figcaption></figure>

### HookDefinition

Each Corresponding Hook is an object containing a _reference_ (pointer) to a `HookDefinition` object.

The HookDefinition object is an unowned reference-counted ledger object that provides for de-duplication of identical web assembly bytecode. Two users using an identical hook will both point to the same HookDefinition.

<figure><img src="../../../.gitbook/assets/spaces_m6f29os4wP16vCS4lHNh_uploads_TlDL7tsVNYi1yU64EZQh_3ef0cee-sethook-Page-2.png" alt=""><figcaption><p>Example: Hook Definitions on Xahau</p></figcaption></figure>

For more information see: [Reference Counting](reference-counted-hook-definitions.md)

### Hook Defaults

When a `HookDefinition` is created it contains the initial [Parameters](parameters.md), [Namespace](namespaces.md) and [Grants](grants.md) supplied by the user. These become the Hook Defaults. Any Hook referencing this Hook Definition will use these defaults _unless_ the SetHook Transaction that creates that reference explicitly overrides those defaults, or a subsequent Update Operation overrides them.

### HookSet Operations

There are six possible operations: No Operation, Create, Update, Delete, Install and Namespace Delete

Each operation is specified by the inclusion or omission of certain HookSet Object fields. This might seem confusing at first but by working through a few examples the reader should find it intuitive; Essentially HookSet operations are a type of **diff** between a specific Hook's _defaults_, _existing_ and newly specified fields.

Achieving each type of operation is explained in a subsection below.

### No Operation

**Occurs when**:

* The HookSet Object is empty

**Behaviour**:

* No change of any kind is made.

**Example**:

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
* No instance of the same web assembly bytecode already exists on Xahau. (If it does and all other requirements are met then interpret as an Install Operation — see below.)

**Behaviour**:

* A reference counted `HookDefinition` object is created on Xahau containing the fields in the HookSet Object, with all specified fields (Namespace, Parameters, HookOn) becoming defaults (but not Grants.)
* A `Hooks` array is created on the executing account, if it doesn't already exist. (This is the structure that contains the Corresponding Hooks.)
* A `Hook` object is created at the Corresponding Hook position if one does not already exist.
* The `Hook` object points at the `HookDefinition`.
* The `Hook` object contains no fields except `HookHash` which points at the created `HookDefinition`.
* If `hsfNSDELETE` flag is specified then any HookState entires in the destination namespace are deleted if they currently exist.

**Example**:

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
* A subset of HookState objects and the HookState directory for the specified namespace are removed from the ledger, up to the defined limit of 512. Further transactions are needed to continue the deletion process until all relevant records are removed.

**Example**:

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
