---
description: Produce an sfEmitDetails suitable for a soon-to-be emitted transaction
---

# etxn\_details

### Concepts

* [Emitted Transactions](../../concepts-and-docs/emitted-transactions.md)

### Behaviour

* Generate and write a 105 byte sfEmitDetails object into the `write_ptr` if cbak is not defined
* Generate and write a 127 byte sfEmitDetails object into the `write_ptr` if cbak is defined.

### Definition

C

```c
int64_t etxn_details (
    uint32_t write_ptr,
  	uint32_t write_len
);
```

### Example

C

```c
uint8_t emitdet[105];
int64_t result =
    etxn_details(emitdet, 105);
if (result != 105)
    rollback("Etxndetails failed.", 19, 1);
```

### Parameters

| Name       | Type      | Description                                              |
| ---------- | --------- | -------------------------------------------------------- |
| write\_ptr | uint32\_t | Pointer to the buffer receiving the sfEmitDetails record |
| write\_len | uint32\_t | Length of the buffer                                     |

### Return Code

| Type     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The number of bytes written.<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.<br><br><code>TOO_SMALL</code><br>- Buffer isn't large enough to receive record<br><br><code>PREREQUISITE_NOT_MET</code><br>- The hook failed to call <code>etxn_reserve(n)</code> first<br><br><code>FEE_TOO_LARGE</code><br>- The burden would be too high for the network to allow.<br><br><code>INTERNAL_ERROR</code><br>- A generic error in which rippled had trouble generating the required field.</p> |
