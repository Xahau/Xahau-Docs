---
description: >-
  Set or delete a parameter on a hook on the same account further down the
  execution chain
---

# hook\_param\_set

### Behaviour

* Search the hook chain on the hook account for a 32 byte hash indicated by `hread_ptr`
* If found: set a parameter:
* With the parameter name indicated by `kread_ptr` and
* The parameter value indicated by `read_ptr`

### Definition

C

```c
int64_t hook_param_set (
    uint32_t read_ptr,
    uint32_t read_len,
    uint32_t kread_ptr,
    uint32_t kread_len,
    uint32_t hread_ptr,
    uint32_t hread_len  
);
```

### Example

C

```c
uint8_t pvalue[] = "some parameter value";
uint8_t pname[] = "paramname";
uint8_t phash[] = { 0x19U, 0xFEU, 0x69U, 0xF1U, 0x53U, 0x66U, 0x4EU, 0x8CU, 
                    0x97U, 0xF4U, 0x4CU, 0x5CU, 0x3CU, 0x65U, 0x63U, 0x79U, 
                    0xC2U, 0xD0U, 0x26U, 0xE7U, 0x90U, 0xEFU, 0x38U, 0xF7U, 
                    0xEDU, 0x73U, 0xE9U, 0xCEU, 0x9CU, 0x9DU, 0xBFU, 0x03U };
int64_t result = 
  	hook_param_set(pvalue, sizeof(pvalue),
                   pname, sizeof(pname),
                   phash, sizeof(phash));
```

### Parameters

| Name       | Type      | Description                     |
| ---------- | --------- | ------------------------------- |
| read\_ptr  | uint32\_t | Pointer to parameter value      |
| read\_len  | uint32\_t | Length of the parameter value   |
| kread\_ptr | uint32\_t | Pointer to the parameter name   |
| kread\_len | uint32\_t | Length of the parameter name    |
| hread\_ptr | uint32\_t | Pointer to hook hash            |
| hread\_len | uint32\_t | Length of hook hash (always 32) |

### Return Code

<table><thead><tr><th width="148">Type</th><th>Description</th></tr></thead><tbody><tr><td>int64_t</td><td>The length of the parameter value successfully set<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.<br><br><code>TOO_SMALL</code><br>- The parameter name can't be null<br><br><code>TOO_BIG</code><br>- The parameter name is greater than 32 bytes</td></tr></tbody></table>
