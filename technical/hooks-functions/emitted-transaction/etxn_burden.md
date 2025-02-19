---
description: Get the burden of a hypothetically emitted transaction
---

# etxn\_burden

### Concepts

* [Emitted Transactions](../../../concepts/emitted-transactions.md)

### Behaviour

* Return the burden an emitted transaction will carry.

### Definition

C

```c
int64_t etxn_burden (
    void
);
```

### Example

C

```c
int64_t burden = 
  etxn_burden();
```

### Parameters

None

### Return Code

<table><thead><tr><th width="165">Type</th><th>Description</th></tr></thead><tbody><tr><td>int64_t</td><td>The burden an emitted transaction will need in order to be successfully passed to <code>emit()</code></td></tr></tbody></table>
