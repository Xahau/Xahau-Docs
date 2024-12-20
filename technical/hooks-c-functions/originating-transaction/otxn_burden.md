---
description: Get the burden of the originating transaction
---

# otxn\_burden

### Behaviour

* Return the burden of the originating transaction or `1` if no burden field is present.

### Definition

C

```c
int64_t otxn_burden (
    void
);
```

### Example

C

```c
int64_t burden = 
  otxn_burden();
```

### Parameters

None

### Return Code

| Type     | Description                                                                                                |
| -------- | ---------------------------------------------------------------------------------------------------------- |
| int64\_t | The burden of the originating transaction, or `1` if no burden was present on the originating transaction. |
