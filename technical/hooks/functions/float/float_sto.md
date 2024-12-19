---
description: Output an XFL as a serialized object
---

# float\_sto

### Concepts

* [Floating Point Numbers (XFL)](../../concepts-and-docs/floating-point-numbers-xfl.md)
* [Serialized Objects](../../concepts-and-docs/serialized-objects.md)

### Behaviour

* Read an XFL floating point number and optionally a field code and currency code
* Write a serialized amount to `write_ptr` according to the parameters provided

### Definition

C

```c
int64_t float_sto (
    uint32_t write_ptr,
    uint32_t write_len,
    uint32_t cread_ptr,
    uint32_t cread_len,  
    uint32_t iread_ptr,
    uint32_t iread_len,  
    int64_t float1,
    uint32_t field_code
);
```

### Example

C

```c
#define SBUF(str) (uint32_t)(str), sizeof(str)
uint8_t amt_out[48];
if (float_sto(SBUF(amt_out),
    SBUF(currency), SBUF(hook_accid), pusd_to_send, -1) < 0)
        rollback(SBUF("Peggy: Could not dump pusd amount into sto"), 1);
```

### Parameters

| Name        | Type      | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ----------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| write\_ptr  | uint32\_t | Pointer to a buffer of a suitable size to store the serialized amount field. Recommend at least 48 bytes.                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| write\_len  | uint32\_t | The length of the output buffer.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| cread\_ptr  | uint32\_t | Pointer to a buffer contianing the currency code to serialize into the output. _May be null._                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| cread\_len  | uint32\_t | The length of the currency code. This must be 20 or 3 or 0 (null).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| iread\_ptr  | uint32\_t | Pointer to a buffer containing the issuer's Account ID to serialize into the output. _May be null._                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| iread\_len  | uint32\_t | The length of the issuer's Account ID. This must be either 20 or 0 (null).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| float1      | int64\_t  | An XFL floating point enclosing number to serialize.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| field\_code | uint32\_t | <p>The <code>sf</code> field code to prefix the serialized amount with. E.g. <code>sfAmount</code>.<br>If this field is <code>0xFFFFFFFFU</code> (i.e. <code>(uint32_t)(-1)</code>) then no field code is prepended to the output, and no issuer or currency code is appended, but serialization proceeds as a floating point amount.<br>If this field is 0 no field code is prepended to the output, and no issuer or currency code is appended, but serialization proceeds as though the amount is an XRP native amount rather than a floating point.</p> |

> ### 📘Hint
>
> To output an `XAH` amount prepopulate the field code in the output buffer then pass the output buffer incremented to the new start and `0` as field\_code

### Return Code

| Type     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The number of bytes written to the output buffer.<br><br>If negative, an error:<br><code>INVALID_FLOAT</code><br>- the supplied float was not a valid XFL enclosing number<br><br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.<br><br><code>INVALID_ARGUMENT</code><br>- If instructed to output as <code>XRP</code> or without <code>field code</code> then all non-write pointers and lengths should be 0 (null).<br><br><code>TOO_SMALL</code><br>- The output buffer was too small to receive the serialized object.<br><br><code>XFL_OVERFLOW</code><br>- Expressing the output caused an overflow during normalization.</p> |
