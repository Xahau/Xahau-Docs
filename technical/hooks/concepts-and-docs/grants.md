---
description: Hook Grants
---

# Grants

> ❗️ Warning
>
> Most Hook Developers will rarely need to use HookGrants, and should exercise extreme caution when granting state mutation permission to foreign Hooks and accounts.
>
> While a HookGrant cannot be used to directly steal funds, intentional external modification of a Hook's State may lead a Hook to behave in an unintended way, which in some cases could lead to a theft.
>
> If you think you need to use a Grant then please re-check your design first to ensure you actually need to use one before continuing.

### Grants

Grants provide a way for a Hook Installer to assign [State Management](state-management.md) permissions to a _foreign_ Hook on other Xahau accounts.

A [SetHook Transaction](sethook-transaction.md) may specify a `HookGrants` array within any `Hook` object in its `Hooks` array. The `HookGrants` array contains one or more `HookGrant` objects (up to 8).

Unlike [Parameters](parameters.md), the `HookGrants` array is always set exactly as specified in the [SetHook Transaction](sethook-transaction.md). Therefore if you wish to update a particular `HookGrant` whilst retaining multiple other `HookGrant` entires that were previously set, you must first obtain the old `HookGrants` array, modify it, and then resubmit the entire array in an [_Update_ Operation](sethook-transaction.md).

To delete all Grants submit an empty `HookGrants` array.

> 🚧 Important
>
> Unlike [Parameters](parameters.md), the `HookGrants` array is always set exactly as specified in the [SetHook Transaction](sethook-transaction.md).

A Grant permits a foreign XRPL account or Hook to modify the Hook State within the namespace of the specific Hook for which the Grant is defined.

The HookGrant must specify at least:

* `HookHash`\
  And may also specify an account:
* `Authorize`

Only the Hook specified by HookHash may modify the Hook State within the namespace of the Hook for which the HookGrant is specified. If `Authorize` is specified then this permission is tightened further to only the Hook specified by the HookHash when it is installed on the account specified by `Authorize`.

> 📘 Tip
>
> Grants only apply to external Hooks and never limit the operation of Hooks with respect to the Hook State on the account they are installed on.

### Example

```json
Account: "rALicebv3hMYNBWtu1VEEWkToArgYsYERs",
TransactionType: "SetHook",
Hooks:
[   
    {   
        Hook: {
            ...,
            HookNamespace: "3963ADEB1B0E8934C0963680531202FD511FF1E16D5864402C2DA63861C420A8",
            HookGrants:
            [   
                {   
                    HookGrant:    // first grant
                    {   
                        HookHash:  "78CAF69EEE950A6C55A450AC2A980DE434D624CD1B13148E007E28B7B6461CC8"
                    },
                    HookGrant:    // second grant
                    {   
                        Authorize: "rCLairev2ma2gNZdcHJeTk7fCQ1ki84vr9",
                        HookHash:  "A5B8D62154DA1C329BE13582086B52612476720CEBD097EB85CEE1455E1C70A6"
                    }
                },  
            ]   
        }   
    }   
],  
... 
```

The _first grant_ above allows:

* any instance of the Hook whose code that hashes to `78CAF69EEE950A6C55A450AC2A980DE434D624CD1B13148E007E28B7B6461CC8`
* executing on **any account**
* to modify the Hook State of account `rALicebv3hMYNBWtu1VEEWkToArgYsYERs`
* inside the Namespace `3963ADEB1B0E8934C0963680531202FD511FF1E16D5864402C2DA63861C420A8`

The _second grant_ above allows:

* any instance of the Hook whose code that hashes to `A5B8D62154DA1C329BE13582086B52612476720CEBD097EB85CEE1455E1C70A6`
* but only when executed on account `rCLairev2ma2gNZdcHJeTk7fCQ1ki84vr9`
* to modify the Hook State of account `rALicebv3hMYNBWtu1VEEWkToArgYsYERs`
* inside the Namespace `3963ADEB1B0E8934C0963680531202FD511FF1E16D5864402C2DA63861C420A8`

### Using the Grant

To make use of a grant, a Hook modifies State objects on a foreign account by calling [state\_foreign\_set](../functions/state/state_foreign_set.md).
