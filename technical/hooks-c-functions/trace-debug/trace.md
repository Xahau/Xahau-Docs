---
description: Write the contents of a buffer to the XRPLD trace log
---

# trace

### Behaviour

* Write a buffer from inside the Hook to the trace log along with a message (if any)

### Definition

C

```c
int64_t trace (
    uint32_t mread_ptr,
    uint32_t mread_len,
    uint32_t dread_ptr,
    uint32_t dread_len,
  	uint32_t as_hex
);
```

### Example

C

```c
#define SBUF(str) (uint32_t)(str), sizeof(str)
trace(SBUF("Buffer contained"), SBUF(some_buffer), 1);
```

### Parameters

| Name       | Type      | Description                                                                                         |
| ---------- | --------- | --------------------------------------------------------------------------------------------------- |
| mread\_ptr | uint32\_t | Pointer to a message to output before the buffer. _May be null._                                    |
| mread\_len | uint32\_t | Length of the message. _May be null._                                                               |
| dread\_ptr | uint32\_t | Pointer to the buffer to output.                                                                    |
| dread\_len | uint32\_t | Length of the buffer to output.                                                                     |
| as\_hex    | uint32\_t | <p>If <code>1</code> output the buffer as hex.<br>If <code>0</code> output the buffer as utf-8.</p> |

### Return Code

| Type     | Description                                                                                                                                             |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p><code>0</code> if successful<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.</p> |
