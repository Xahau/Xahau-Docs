---
description: >-
  Parse the STI_AMOUNT in the specified slot and return it as an XFL enclosed
  number
---

# slot\_float

### Behaviour

* Parse the STI\_AMOUNT in the specified slot and return it as an XFL enclosed number

### Definition

C

```c
int64_t slot_float (
    uint32_t slot_no
);
```

### Example

C

```c
int64_t xfl =
  	slot_float(amt_slot);
```

### Parameters

| Name     | Type      | Description     |
| -------- | --------- | --------------- |
| slot\_no | uint32\_t | The slot number |

### Return Code

| Type     | Description                                                                                                                                                                                                                                                                          |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| int64\_t | <p>The XFL enclosing number<br><br>If negative, an error:<br><code>DOESNT_EXIST</code><br>- the specified slot does not contain any object or it is an invalid slot<br><br><code>NOT_AN_AMOUNT</code><br>- the specified slot does not contain an <code>STI_AMOUNT</code> object</p> |
