---
description: Count the elements of an array object in a slot
---

# slot\_count

### Behaviour

* Count the elements of an array in the specified slot
* Return the count

### Definition

C

```c
int64_t slot_count (
    uint32_t slot_no
);
```

### Example

C

```c
slot_count(1); // assumes an array is slotted into slot=1
```

### Parameters

| Name     | Type      | Description     |
| -------- | --------- | --------------- |
| slot\_no | uint32\_t | The slot number |

### Return Code

| Type     | Description                                                                                                                                                                                                                                                                              |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The number of elements inside the slotted array<br><br>If negative, an error:<br><code>DOESNT_EXIST</code><br>- the specified slot does not contain any object or it is an invalid slot<br><br><code>NOT_AN_ARRAY</code><br>- the specified slot does not contain an array object</p> |
