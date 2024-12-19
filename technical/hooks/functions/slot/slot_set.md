---
description: Locate an object based on its keylet and place it into a slot
---

# slot\_set

### Behaviour

* Locate an object given the Keylet provided in `read_ptr`
* Emplace the located object into the slot specified or into a new slot if no slot (zero) is specified

### Definition

C

```c
int64_t slot_set (
    uint32_t read_ptr,
    uint32_t read_len,
  	uint32_t slot_no
);
```

### Example

C

```c
int64_t slot_no = 
  slot_set(keylet, 34, 0);
```

### Parameters

| Name      | Type      | Description                                                                                     |
| --------- | --------- | ----------------------------------------------------------------------------------------------- |
| read\_ptr | uint32\_t | Pointer to a buffer containing the keylet of the object to locate. This can also be a txn hash. |
| read\_len | uint32\_t | Length of the read buffer. Should always be 32 or 34.                                           |
| slot\_no  | uint32\_t | The slot number to emplace into, or 0 if you wish to pick the next available.                   |

### Return Code

| Type     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The slot number the object was inserted into<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.<br><br><code>INVALID_ARGUMENT</code><br>- <code>read_len</code> must be either 32 or 34 bytes depending on whether a txn hash or a keylet is being used in <code>read_ptr</code><br>- the hash or keylet was invalid<br><br><code>DOESNT_EXIST</code><br>- the requested object was not found</p> |
