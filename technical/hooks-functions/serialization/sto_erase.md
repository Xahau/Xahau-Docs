---
description: Remove a field from an STObject
---

# sto\_erase

### Concepts

* [Serialized Objects](../../../concepts/serialized-objects.md)

### Behaviour

{% tabs %}
{% tab title="C" %}
* Parse an STObject pointed to by `read_ptr`
* Write a new STObject to `write_ptr` but without `field_id` if it was present in the original object.
{% endtab %}

{% tab title="Javascript" %}
* It will look for the STO object (binary encoded ledger data) from which the field will be removed.
* It will look for the ID of the field to be erased.
* Returns the updated STO object in binary encoded ledger data format, or an error code if the operation fails.
{% endtab %}
{% endtabs %}

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t sto_erase (
    uint32_t write_ptr,
    uint32_t write_len,
    uint32_t read_ptr,
    uint32_t read_len,
    uint32_t field_id
);
```

> ### 🚧Field ID encoding
>
> The `sto_` apis accept a `field_id` parameter encoded as follows: `(type << 16U) + field`\
> Thus type 1 field 2 would be `0x10002U`.
{% endtab %}

{% tab title="Javascript" %}
```javascript
function sto_erase(
    sto: ByteArray | HexString,
    field_id: number
  ): ErrorCode | ByteArray
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t result = 
  sto_erase(tx_out, sizeof(tx_out),
            tx_in, tx_len, sfSigners);

if (tx_len <= 0)
    rollback("Erasing failed.", 15, 1);
```

> ### 📘Emplace equivalence
>
> `sto_erase` is the same as `sto_emplace` with `0,0` for `field_ptr, field_len` parameters.
{% endtab %}

{% tab title="Javascript" %}
```javascript
const tx_out = sto_erase(tx_in, sfSigners)

if (typeof tx_out === 'number')
    rollback("Erasing failed.", 1)
```
{% endtab %}
{% endtabs %}

### Parameters

{% tabs %}
{% tab title="C" %}
| Name       | Type      | Description                                  |
| ---------- | --------- | -------------------------------------------- |
| write\_ptr | uint32\_t | The buffer to write the modified STObject to |
| write\_len | uint32\_t | The length of the output buffer              |
| read\_ptr  | uint32\_t | The buffer to read the source STObject from  |
| read\_len  | uint32\_t | The Length of the source object              |
| field\_id  | uint32\_t | The `sf` code (location) to erase            |


{% endtab %}

{% tab title="Javascript" %}
| Name      | Type                   | Description                                                                       |
| --------- | ---------------------- | --------------------------------------------------------------------------------- |
| sto       | ByteArray \| HexString | The STO object (binary encoded ledger data) from which the field will be removed. |
| field\_id | number                 | The ID of the field to be erased.                                                 |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The number of bytes written to <code>write_ptr</code><br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.<br><br><code>TOO_SMALL</code><br>- Output buffer must be at least as large as the source object.<br><br><code>TOO_BIG</code><br>- Field you are attempting to erase from is too large<br><br><code>PARSE_ERROR</code><br>- The supplied STObject is malformed or not an STObject.<br><br><code>DOESNT_EXIST</code><br>- The specified <code>field_id</code> isn't present in the STObject.</p> |


{% endtab %}

{% tab title="Javascript" %}
| Type                   | Description                                                                                           |
| ---------------------- | ----------------------------------------------------------------------------------------------------- |
| ErrorCode \| ByteArray | The updated STO object in binary encoded ledger data format, or an error code if the operation fails. |
{% endtab %}
{% endtabs %}

