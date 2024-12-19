---
description: Retreive the 32 byte namespace biased SHA512H of the currently executing Hook
---

# hook\_hash

### Behaviour

* Look up the hash of the hook installed on hook account at position `hook_no`
* Write the 32 byte hash to `write_ptr`

### Definition

C

```c
int64_t hook_hash (
    uint32_t write_ptr,
    uint32_t write_len,
  	int32_t  hook_no
);
```

### Example

C

```c
uint8_t hash[32];
int64_t bytes_written = 
    hook_hash(hash, 32, -1);
```

### Parameters

| Name       | Type      | Description                                                                                    |
| ---------- | --------- | ---------------------------------------------------------------------------------------------- |
| write\_ptr | uint32\_t | Pointer to a buffer of a suitable size to store the output. Should be at least 32 bytes.       |
| write\_len | uint32\_t | Length of the output buffer.                                                                   |
| hook\_no   | int32\_t  | The position in the hook chain the hook is located at, or -1 for the currently executing hook. |

### Return Code

| Type     | Description                                                                                                                                                                                                                                                      |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The number of bytes written<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.<br><br><code>DOESNT_EXIST</code><br>- The specified hook sequence number doesn't exist in the hook chain.</p> |
