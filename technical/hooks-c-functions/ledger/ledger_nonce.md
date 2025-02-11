---
description: Generate a 32 byte nonce for use in an emitted transaction
---

# ledger\_nonce

### Behaviour

* Write a 32 byte random value to the write\_ptr

### Definition

C

```c
int64_t ledger_nonce (
    uint32_t write_ptr,
    uint32_t write_len
);
```

### Example

C

```c
uint8_t n[32];
int64_t bytes_written = 
    ledger_nonce(n, 32);
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
