---
description: >-
  Index into a xahaud serialized object and return the location and length of a
  subfield
---

# sto\_subfield

### Concepts

* [Serialized Objects](../../concepts-and-docs/serialized-objects.md)

### Behaviour

* Parse a STObject pointed to by `read_ptr`
* Find the field specified by `field_id`
* If the field is found, and:
*
  1. It is an array, then return the start and length of the array including the leadin/leadout bytes, or
*
  2. It is **not** an array, then return the start and length of the PAYLOAD of the field (excluding the leadin bytes).

> ### 🚧Field ID encoding
>
> The `sto_` apis accept a `field_id` parameter encoded as follows: `(type << 16U) + field`\
> Thus type 1 field 2 would be `0x10002U`.

### Definition

C

```c
int64_t sto_subfield (
    uint32_t read_ptr,
  	uint32_t read_len,
  	uint32_t field_id
);
```

### Example

C

```c
#define SUB_OFFSET(x) ((int32_t)(x >> 32))
#define SUB_LENGTH(x) ((int32_t)(x & 0xFFFFFFFFULL))
int64_t memo_lookup =
    sto_subfield(memo_ptr, memo_len, sfMemo);
if (memo_lookup < 0)
{
    // sfMemo was not found in the STObject pointed at by memo_ptr
}
else
{
    // sfMemo was found and its location is as follows:
	  uint8_t* memo_ptr = SUB_OFFSET(memo_lookup) + memo_ptr;
	  int64_t  memo_len = SUB_LENGTH(memo_lookup);
}
```

> ### 📘
>
> hookmacro.h already contains the `SUB_OFFSET` and `SUB_LENGTH` macros.

### Parameters

| Name      | Type      | Description                                                                                                                                                                                                                                                                                                                                                                                                |
| --------- | --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| read\_ptr | uint32\_t | Pointer to the buffer containing the STObject                                                                                                                                                                                                                                                                                                                                                              |
| read\_len | uint32\_t | Length of STObject                                                                                                                                                                                                                                                                                                                                                                                         |
| field\_id | uint32\_t | <p>The <code>sf</code> code of the field you are searching for.<br><br>To compute this manually take the serialized <code>type</code> and shift it into the 16 highest bits of uint32_t, then take the <code>field</code> and place it in the 16 lowest bits.<br><br>For example:<br><code>sfEmitNonce</code> has <code>type</code> 5 and <code>field</code> 11 thus its value is <code>0x050BU</code></p> |

### Return Code

| Type     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The location of the field within the specified buffer:<br>- The high 32 bits are the offset location.<br>- The low 32 bits are the length.<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.<br><br><code>TOO_SMALL</code><br>- Input buffer isn't large enough to possibly contain a valid STObject.<br><br><code>DOESNT_EXIST</code><br>- The searched for field isn't present in the supplied STObject.<br><br><code>PARSE_ERROR</code><br>- The supplied STObject is malformed or not an STObject.</p> |
