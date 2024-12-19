---
description: Fetch the fee base of the current ledger
---

# fee\_base

### Concepts

* [Hook Fees](../../concepts-and-docs/hook-fees.md)

### Behaviour

* Return the fee base from the current ledger

### Definition

C

```c
int64_t fee_base ();
```

### Example

C

```c
int64_t fee =
    fee_base();
```

### Parameters

This API takes no parameters.

### Return Code

| Type     | Description                        |
| -------- | ---------------------------------- |
| int64\_t | The fee base of the current ledger |
