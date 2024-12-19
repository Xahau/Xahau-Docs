---
description: Convert an r-address into a 20 byte Account ID
---

# util\_accid

### Behaviour

* Read an r-address from the `read_ptr`
* Write a 20 byte Account ID to the `write_ptr`

### Definition

C

```c
int64_t util_accid (
    uint32_t write_ptr,
    uint32_t write_len,
    uint32_t read_ptr,
    uint32_t read_len
);
```

### Example

C

```c
uint8_t accid_out[20];
uint8_t raddr_in[] = "rHb9CJAWyB4rj91VRWn96DkukG4bwdtyTh";

int64_t bytes_written = 
    util_accid(accid_out, 20, raddr_in, sizeof(raddr_in)-1);
// NB: if specified as a c-string as above, account for the nul char
```

### Parameters

<table><thead><tr><th>Name</th><th width="102">Type</th><th>Description</th></tr></thead><tbody><tr><td>write_ptr</td><td>uint32_t</td><td>Pointer to a buffer of a suitable size to store the output Account ID. Must be at least 20 bytes.</td></tr><tr><td>write_len</td><td>uint32_t</td><td>Length of the output buffer.</td></tr><tr><td>read_ptr</td><td>uint32_t</td><td>Pointer to the r-address.</td></tr><tr><td>read_len</td><td>uint32_t</td><td>The length of the r-address.</td></tr></tbody></table>

### Return Code

| Type     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| int64\_t | <p>The number of bytes written (the length of the output r-address).<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.<br><br><code>INVALID_ARGUMENT</code><br>- <code>read_ptr</code> pointed at something which wasn't a valid r-address.<br><br><code>TOO_SMALL</code><br>- <code>write_len</code> was not large enough to store produced Account ID. (Should be 20 bytes).<br><br><code>TOO_BIG</code><br>- <code>read_len</code> was longer than an r-address can be.</p> |
