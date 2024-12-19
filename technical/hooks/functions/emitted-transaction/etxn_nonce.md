---
description: Generate a 32 byte nonce for use in an emitted transaction
---

# etxn\_nonce

### Concepts

* [Emitted Transactions](../../concepts-and-docs/emitted-transactions.md)

### Behaviour

* Write the 32 byte Hash to the write\_ptr

### Definition

C

```c
int64_t etxn_nonce (
    uint32_t write_ptr,
    uint32_t write_len
);
```

### Example

C

```c
uint8_t n[32];
int64_t bytes_written = 
    etxn_nonce(n, 32);
```

### Parameters

| Name       | Type      | Description                                                                              |
| ---------- | --------- | ---------------------------------------------------------------------------------------- |
| write\_ptr | uint32\_t | Pointer to a buffer of a suitable size to store the output. Should be at least 32 bytes. |
| write\_len | uint32\_t | Length of the output buffer.                                                             |

### Return Code

<table><thead><tr><th width="187">Type</th><th>Description</th></tr></thead><tbody><tr><td>int64_t</td><td>The number of bytes written<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.</td></tr></tbody></table>
