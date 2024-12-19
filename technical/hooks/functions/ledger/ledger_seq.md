---
description: Fetch the current ledger sequence number
---

# ledger\_seq

### Behaviour

* Return the sequence number from the current ledger

### Definition

C

```c
int64_t ledger_seq ();
```

### Example

C

```c
int64_t seq =
    ledger_seq();
```

### Parameters

This API takes no parameters.

### Return Code

| Type     | Description                               |
| -------- | ----------------------------------------- |
| int64\_t | The sequence number of the current ledger |
