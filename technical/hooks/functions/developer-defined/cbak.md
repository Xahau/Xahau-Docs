---
description: The callback function of your hook
---

# cbak

### Concepts

* [Compiling Hooks](../../concepts-and-docs/compiling-hooks.md)

### Behaviour

* `cbak` is a user defined function called by `xahaud` in order to inform your hook about the status of a previously emitted transaction
* State changes and further emit calls can be made from cbak but it cannot `rollback` a transaction.
* When cbak is executed the emitted transaction to which the callback relates is now the originating transaction.

### Definition

C

```c
int64_t cbak (
    uint32_t what
)
```

### Example

C

```c
int64_t cbak(uint32_t what)
{
    return 0;
}
```

### Parameters

| Name | Type      | Description                                                                                                                                                                                                                                                                        |
| ---- | --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| what | uint32\_t | <p>if <code>0</code>:<br>- the emittted transaction to which this callback relates was successfully accepted into a ledger.<br><br>If <code>1</code><br>- the emitted transaction to which the callback relates was NOT successfully accepted into a ledger before it expired.</p> |

### Return Code

| Type     | Description                                                                                                                      |
| -------- | -------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | An arbitrary return code you wish to return from your hook. This will be present in the metadata of the originating transaction. |
