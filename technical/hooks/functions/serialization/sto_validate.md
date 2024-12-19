---
description: Validate an STObject
---

# sto\_validate

### Concepts

* [Serialized Objects](../../concepts-and-docs/serialized-objects.md)

### Behaviour

* Parse an STObject pointed to by `read_ptr`
* Return 1 if the serialization is valid, 0 otherwise.

### Definition

C

```c
int64_t sto_validate (
    uint32_t read_ptr,
    uint32_t read_len
);
```

### Example

C

```c
int64_t result = 
  sto_validate(tx_out, sizeof(tx_out));

if (tx_len <= 0)
    rollback("Invalid STO.", 12, 1);
```

### Parameters

| Name      | Type      | Description                                 |
| --------- | --------- | ------------------------------------------- |
| read\_ptr | uint32\_t | The buffer to read the source STObject from |
| read\_len | uint32\_t | The Length of the source object             |

### Return Code

| Type     | Description                                                                                                                                                                                                                                       |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p><code>1</code> if the STObject pointed to by <code>read_ptr</code> is a valid STObject.<br><code>0</code> if it isn't.<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.</p> |
