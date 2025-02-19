---
description: Prevent state clobbering by using the correct namespace
---

# Namespaces

### Namespaces

To avoid two or more Hooks installed on the same account unintentionally clobbering each-other's [Hook State](state-management.md), a 32 byte namespace must be provided when creating or installing each Hook.

The namespace may be any arbitrary 32 byte value the developer chooses. Provided the namespace is unique in the Hook chain no state clobbering will occur.

We strongly recommended using `SHA256` over the developer's working name for the Hook. SHA256 is one of the two hashing algorithms used in the derivation of Xahau addresses (from an account master key), and, as such, it should be readily available to the developer.

The `HookNamespace` field is supplied as a 32 byte _hex_ blob inside each `Hook` object in a `Hooks` array when [executing a SetHook transaction](sethook-transaction.md).

The configured Namespace a Hook operates under alters the [Keylets](slots-and-keylets.md) its [State](state-management.md) is stored under. Therefore two Hooks under two different Namespaces installed on the same Xahau account may use the same state key to refer to different state objects. Conversely, two different Hooks using the same Namespace on the same Xahau account can access and modify eachother's state objects using the same state keys.

### Example

In javascript, importing the `ripple-address-codec` yields access to SHA256.\
(It is also possible to use `crypto.subtle` in browser, or `crypto.createHash` in node to access this hash algorithm.)

```js
HookNamespace: addr.codec.sha256('carbon').toString('hex')
```

### Default Namespace

The first user to [set a novel Hook](sethook-transaction.md) defines a `HookNamespace` which becomes the _Default Namespace_ for that Hook. This means any subsequent users who [reference the same _HookDefinition_](reference-counted-hook-definitions.md) will receive this originally set Namespace by default.

The subsequent user may specify their own Namespace, overriding the Default Namespace for their installation only.

### Hook APIs Affected

Choice of HookNamespace affects the behaviour of the following Hook APIs:

* [state](../technical/hooks-functions/state/)
* [state\_set](../technical/hooks-functions/state/state_set.md)

### Namespace API Helper

See [account\_info](../technical/hooks-functions/websocket-apis/account_info.md) and [account\_namespace](../technical/hooks-functions/websocket-apis/account_namespace.md) for information about how to query the ledger regarding namespaces.
