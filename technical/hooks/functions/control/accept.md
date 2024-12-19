---
description: Accept the originating transaction and commit any changes the hook made.
---

# accept

### Concepts

* [Introduction](../../concepts-and-docs/introduction/)
* Execution Order

### Behaviour

End the execution of the hook with status: success.

* Record a return string and return code in transaction metadata.
* Commit all state changes.
* Submit all `emit()` transactions.
* Allow originating transaction to continue.

> ### 🚧Caution
>
> If the originating transaction is stopped for some other reason then this accept becomes a rollback. See: Execution Order.

### Definition

C

```c
int64_t accept (
    uint32_t read_ptr,
    uint32_t read_len,
    uint64_t error_code
);
```

### Example

C

```c
accept("Success", 7, 100);
```

### Parameters

| Name        | Type      | Description                                                                                                                                                                         |
| ----------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| read\_ptr   | uint32\_t | <p>Pointer to a return string to be stored in execution metadata.<br>This is any string the hook-developer wishes to return with the acceptance. <em>May be null.</em></p>          |
| read\_len   | uint32\_t | The length of the return string. At most 32. _May be null._                                                                                                                         |
| error\_code | uint64\_t | <p>A return code specific to this hook to be stored in execution metadata.<br><br>Similar to the return code of an application on a *nix system. By convention success is zero.</p> |

### Return Code

| Type     | Description                                                                                                                                             |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | Accept ends the hook, therefore no value is returned to the caller. By convention all Hook APIs return `int64_t`, but in this case nothing is returned. |
