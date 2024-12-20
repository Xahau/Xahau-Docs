---
description: Retreive the 32 byte namespace biased SHA512H of the last closed ledger
---

# ledger\_last\_hash

### Behaviour

* Write the 32 byte Hash to the write\_ptr

### Definition

C

```c
int64_t ledger_last_hash (
    uint32_t write_ptr,
    uint32_t write_len
);
```

### Example

C

```c
uint8_t hash[32];
int64_t bytes_written = 
    ledger_last_hash(hash, 32);
```

### Parameters

| Name       | Type      | Description                                                                              |
| ---------- | --------- | ---------------------------------------------------------------------------------------- |
| write\_ptr | uint32\_t | Pointer to a buffer of a suitable size to store the output. Should be at least 32 bytes. |
| write\_len | uint32\_t | Length of the output buffer.                                                             |

### Return Code

| Type     | Description                                                                                                                                            |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| int64\_t | <p>The number of bytes written<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.</p> |
