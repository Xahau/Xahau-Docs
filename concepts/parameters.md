---
description: Install-time parameters allow Hooks to be generic and flexible
---

# Parameters

### Parameters

Hook developers may opt to use _install-time_ parameters (called Hook Parameters) in their Hook. This allows subsequent installers of the Hook to change certain behaviours the programmer defines without recompiling or re-uploading the Hook (assuming at least one account still [references](reference-counted-hook-definitions.md) the existing Hook Definition.)

Hook Parameters are a set of Key-Value pairs set during the [SetHook Transaction](sethook-transaction.md) and retrievable by the Hook during runtime. Both the `ParameterName` (key) and the `ParameterValue` are set as _hex_ blobs, and have a maximum length of 32 bytes and 256 bytes respectively.

A [SetHook Transaction](sethook-transaction.md) may define up to _16_ Hook Parameters per installed Hook.

### Setting Parameters

The `HookParameters` array is optionally defined inside each `Hook` in the `Hooks` array as shown below:

```json
TransactionType: "SetHook",
Hooks:
[   
    {   
        Hook: {
            ...,
            HookParameters:
            [   
                {   
                    HookParameter:
                    {   
                        HookParameterName:  "ABCDEF12",
                        HookParameterValue: "12345678"
                    }   
                },  
                ...  // optionally up to 15 more Hook Parameters
            ]   
        }   
    }   
],  
... 
```

### Default Parameters

The first user to [set a novel Hook](sethook-transaction.md) may define Hook Parameters which then become the _Default Parameters_ for that Hook. This means any subsequent users who [references the same _HookDefinition_](reference-counted-hook-definitions.md) will receive these originally set Hook Parameters by default.

The subsequent user may specify their own Parameters, overriding the Default Parameters for their installation.

To erase a Parameter in a subsequent installation, specify the `ParameterName` key without specifying a `ParameterValue` key.

### Using Parameters in Hooks

Parameters can be read by the Hooks they are set on using [hook\_param](../technical/hooks-functions/hook-context/hook_param.md).

If more than one Hook is installed in a Hook Chain, then [hook\_param\_set](../technical/hooks-functions/hook-context/hook_param_set.md) can be used in limited circumstances to modify the Hook Parameters of a Hook further down the chain on the same account.

### Runtime Parameters

On Xahau and the Xahau testnet, HookParameters may also be included at the top level of any transaction type according to the foregoing rules and size limits. These parameters can be accessed inside a hook using the [otxn\_param](../technical/hooks-functions/originating-transaction/otxn_param.md) API.
