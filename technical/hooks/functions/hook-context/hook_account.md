---
description: Retreive the 20 byte Account ID the Hook is executing on
---

# hook\_account

### Behaviour

* Write the 20 byte Account ID to the write\_ptr

### Definition

C

```c
int64_t hook_account (
    uint32_t write_ptr,
    uint32_t write_len
);
```

### Example

C

```c
uint8_t hook_acc_id[20];
int64_t bytes_written = 
    hook_account(hook_acc_id, 20);
```

### Parameters

| Name       | Type      | Description                                                                              |
| ---------- | --------- | ---------------------------------------------------------------------------------------- |
| write\_ptr | uint32\_t | Pointer to a buffer of a suitable size to store the output. Should be at least 20 bytes. |
| write\_len | uint32\_t | Length of the output buffer.                                                             |

### Return Code

| Type     | Description                                                                                                                                            |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| int64\_t | <p>The number of bytes written<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.</p> |
