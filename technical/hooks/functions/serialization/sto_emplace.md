---
description: Emplace a field into an existing STObject at its canonical placement
---

# sto\_emplace

### Concepts

* [Serialized Objects](../../concepts-and-docs/serialized-objects.md)

### Behaviour

* Parse an STObject `S` (source object) pointed to by `sread_ptr`
* Parse an STObject `F` (to inject/emplace) pointed to by `fread_ptr`
* Write a new STObject to `write_ptr` which places `F` into `S` at the canonical position `field_id`

> ### 🚧Field ID encoding
>
> The `sto_` apis accept a `field_id` parameter encoded as follows: `(type << 16U) + field`\
> Thus type 1 field 2 would be `0x10002U`.

### Definition

C

```c
int64_t sto_emplace (
    uint32_t write_ptr,
  	uint32_t write_len,
    uint32_t sread_ptr,
    uint32_t sread_len,
    uint32_t fread_ptr,
    uint32_t fread_len,
  	uint32_t field_id
);
```

### Example

C

```c
uint8_t tx_out[1024];

int64_t tx_len =
    sto_emplace(tx_out, sizeof(tx_out),
                tx_in, tx_len,
                sequence_field, 5, sfSequence);

if (tx_len <= 0)
    rollback("Emplacing failed.", 17, 1);
```

### Parameters

| Name       | Type      | Description                                                                                                                                                             |
| ---------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| write\_ptr | uint32\_t | The buffer to write the modified STObject to                                                                                                                            |
| write\_len | uint32\_t | The length of the output buffer                                                                                                                                         |
| sread\_ptr | uint32\_t | The buffer to read the source STObject from                                                                                                                             |
| sread\_len | uint32\_t | The Length of the source object                                                                                                                                         |
| fread\_ptr | uint32\_t | The buffer to read the field to be emplaced/injected from                                                                                                               |
| fread\_len | uint32\_t | The length of the field to be emplaced/injected                                                                                                                         |
| field\_id  | uint32\_t | The `sf` code (location) to form the emplacement. If this already exists in the source object then the existing field is overriden. If it doesn't exist it is inserted. |

### Return Code

<table><thead><tr><th width="169">Type</th><th>Description</th></tr></thead><tbody><tr><td>int64_t</td><td>The number of bytes written to <code>write_ptr</code><br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.<br><br><code>TOO_SMALL</code><br>- Output buffer must be at least as large as the source object + the injected field, even if the field is only being overriden.<br><br><code>TOO_BIG</code><br>- Field you are attempting to emplace is too large<br><br><code>PARSE_ERROR</code><br>- The supplied STObject is malformed or not an STObject.</td></tr></tbody></table>
