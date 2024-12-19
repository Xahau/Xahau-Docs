---
description: Get the generation of a hypothetically emitted transaction
---

# etxn\_generation

### Concepts

* [Emitted Transactions](../../concepts-and-docs/emitted-transactions.md)

### Behaviour

* Return the generation an emitted transaction will carry.

### Definition

C

```c
int64_t etxn_generation (
    void
);
```

### Example

C

```c
int64_t burden = 
  etxn_generation();
```

### Parameters

None

### Return Code

| Type     | Description                                                                                    |
| -------- | ---------------------------------------------------------------------------------------------- |
| int64\_t | The generation an emitted transaction will need in order to be successfully passed to `emit()` |
