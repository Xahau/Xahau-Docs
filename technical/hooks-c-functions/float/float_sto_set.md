---
description: Read a serialized amount into an XFL
---

# float\_sto\_set

### Concepts

* [Floating Point Numbers (XFL)](../../../concepts/floating-point-numbers-xfl.md)
* [Serialized Objects](../../../concepts/serialized-objects.md)

### Behaviour

* Read a serialized floating point number.
* If there are more fields/data after the serialized floating pointer number then ignore them.
* Return it as an XFL enclosing number

### Definition

C

```c
int64_t float_sto_set (
    uint32_t read_ptr,
    uint32_t read_len
);
```

### Example

C

```c
int64_t vault_pusd = float_sto_set(vault, 8);
if (vault_pusd < 0)
  rollback("Failed to parse serialized float.", 33, 1);
```

### Parameters

| Name      | Type      | Description                                                       |
| --------- | --------- | ----------------------------------------------------------------- |
| read\_ptr | uint32\_t | Pointer to a buffer contianing the serialized XFL. _May be null._ |
| read\_len | uint32\_t | The length of the buffer.                                         |

### Return Code

| Type     | Description                                                                                                                                                                                                                                                                                      |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| int64\_t | <p>The number of bytes written to the output buffer.<br><br>If negative, an error:<br><code>NOT_AN_OBJECT</code><br>- the supplied buffer did not contain a valid serialized floating point number<br><br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.</p> |
