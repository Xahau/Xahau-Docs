---
description: >-
  Index into a xahaud serialized array and return the location and length of an
  index
---

# sto\_subarray

### Concepts

* [Serialized Objects](../../../concepts/serialized-objects.md)

### Behaviour

* Parse a STArray pointed to by `read_ptr`
* Find the array index specified by `array_id`
* Return the byte offset and length of the serialized field within the STObject, if it is found

> ### 🚧Field ID encoding
>
> The `sto_` apis accept a `field_id` parameter encoded as follows: `(type << 16U) + field`\
> Thus type 1 field 2 would be `0x10002U`.
>
> In the case of this array field ID is `array_id`.

### Definition

C

```c
int64_t sto_subfield (
    uint32_t read_ptr,
  	uint32_t read_len,
  	uint32_t array_id
);
```

### Example

C

```c
#define SUB_OFFSET(x) ((int32_t)(x >> 32))
#define SUB_LENGTH(x) ((int32_t)(x & 0xFFFFFFFFULL))

  int64_t memo_lookup =
    sto_subarray(memos, memos_len, 0);

if (memo_lookup < 0)
{
    // sfMemo was not found in the STObject pointed at by memo_ptr
}
else
{
    // 0th index of the STArray was found and its location is as follows:
    uint8_t*  memo_ptr = SUB_OFFSET(memo_lookup) + memos;
    uint32_t  memo_len = SUB_LENGTH(memo_lookup);
}
```

> ### 📘
>
> hookmacro.h already contains the `SUB_OFFSET` and `SUB_LENGTH` macros.

### Parameters

| Name      | Type      | Description                                                               |
| --------- | --------- | ------------------------------------------------------------------------- |
| read\_ptr | uint32\_t | Pointer to the buffer containing the STArray                              |
| read\_len | uint32\_t | Length of STArray                                                         |
| array\_id | uint32\_t | The index of the entry within the STArray you are seeking. Starts from 0. |

### Return Code

| Type     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The location of the field within the specified buffer:<br>- The high 32 bits are the offset location.<br>- The low 32 bits are the length.<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.<br><br><code>TOO_SMALL</code><br>- Input buffer isn't large enough to possibly contain a valid STArray.<br><br><code>DOESNT_EXIST</code><br>- The searched for index isn't present in the supplied STArray.<br><br><code>PARSE_ERROR</code><br>- The supplied STArray is malformed or not an STArray.</p> |
