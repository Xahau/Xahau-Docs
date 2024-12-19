---
description: Get the generation of the originating transaction
---

# otxn\_generation

### Behaviour

* Return the generation of the originating transaction or `1` if no generation field is present.

### Definition

C

```c
int64_t otxn_generation (
    void
);
```

### Example

C

```c
int64_t generation = 
  otxn_generation();
```

### Parameters

None

### Return Code

| Type     | Description                                                                                                        |
| -------- | ------------------------------------------------------------------------------------------------------------------ |
| int64\_t | The generation of the originating transaction, or `1` if no generation was present on the originating transaction. |
