---
description: Compute the serialized size of an object in a slot
---

# slot\_size

### Behaviour

* Return the number of bytes the object in the specified slot occupies when serialized

### Definition

C

```c
int64_t slot_size (
    uint32_t slot_no
);
```

### Example

C

```c
int64_t bytes_needed = slot_size(1); // get size of slot 1
```

### Parameters

| Name     | Type      | Description     |
| -------- | --------- | --------------- |
| slot\_no | uint32\_t | The slot number |

### Return Code

| Type     | Description                                                                                                                                                                                            |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| int64\_t | <p>The number of bytes the object occupies when serialized<br><br>If negative, an error:<br><code>DOESNT_EXIST</code><br>- the specified slot does not contain any object or it is an invalid slot</p> |
