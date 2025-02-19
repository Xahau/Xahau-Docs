---
description: Free up a currently occupied slot
---

# slot\_clear

### Behaviour

* Free the specified slot, releasing any object that was slotted there

### Definition

C

```c
int64_t slot_clear (
    uint32_t slot_no
);
```

### Example

C

```c
slot_clear(1); // assumes a transaction is slotted into slot=1
```

### Parameters

| Name     | Type      | Description     |
| -------- | --------- | --------------- |
| slot\_no | uint32\_t | The slot number |

### Return Code

| Type     | Description                                                                                                                                                               |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p><code>1</code> or an error<br><br>If negative, an error:<br><code>DOESNT_EXIST</code><br>- the specified slot does not contain any object or it is an invalid slot</p> |
