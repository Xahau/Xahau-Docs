# rollback

### Concepts

* [Introduction](../../concepts-and-docs/introduction/)
* Execution Order

### Behaviour

End the execution of the hook with status: reject.

* Record a return string and return code in transaction metadata.
* Discard all state changes.
* Discard all `emit()` transactions.
* Disallow originating transaction to continue.

> ### ❗️Warning
>
> The originating transaction will fail with `tecHOOK_REJECTED` and a fee will be charged. See: Execution Order.

### Definition

C

```c
int64_t rollback (
    uint32_t read_ptr,
    uint32_t read_len,
    uint64_t error_code
);
```

### Example

C

```c
rollback("Rejected!", 9, 100);
```

### Parameters

<table><thead><tr><th>Name</th><th>Type</th><th width="202">Description</th></tr></thead><tbody><tr><td>read_ptr</td><td>uint32_t</td><td>Pointer to a return string to be stored in execution metadata.<br>This is any string the hook-developer wishes to return with the acceptance. <em>May be null.</em></td></tr><tr><td>read_len</td><td>uint32_t</td><td>The length of the return string. At most 32. <em>May be null.</em></td></tr><tr><td>error_code</td><td>uint64_t</td><td>A return code specific to this hook to be stored in execution metadata.<br><br>Similar to the return code of an application on a *nix system. By convention non-success is non-zero.</td></tr></tbody></table>

### Return Code

<table><thead><tr><th width="123">Type</th><th>Description</th></tr></thead><tbody><tr><td>int64_t</td><td>Rollback ends the hook, therefore no value is returned to the caller. By convention all Hook APIs return <code>int64_t</code>, but in this case nothing is returned.</td></tr></tbody></table>
