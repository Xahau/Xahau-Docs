---
description: Emplace a field into an existing STObject at its canonical placement
---

# sto\_emplace

### Concepts

* [Serialized Objects](../../../concepts/serialized-objects.md)

### Behaviour

{% tabs %}
{% tab title="C" %}
* Parse an STObject `S` (source object) pointed to by `sread_ptr`
* Parse an STObject `F` (to inject/emplace) pointed to by `fread_ptr`
* Write a new STObject to `write_ptr` which places `F` into `S` at the canonical position `field_id`

> ### 🚧Field ID encoding
>
> The `sto_` apis accept a `field_id` parameter encoded as follows: `(type << 16U) + field`\
> Thus type 1 field 2 would be `0x10002U`.
{% endtab %}

{% tab title="Javascript" %}
* Ask for the STO object by the param `sto`
* Ask for the bytes representing the field to be added by the param `field_bytes`
* Ask for the ID of the field to be added by the param `field_id`
* Return the updated STO object in binary encoded ledger data format, or an error code if the operation fails.
{% endtab %}
{% endtabs %}

### Definition

C

{% tabs %}
{% tab title="C" %}
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


{% endtab %}

{% tab title="Javascript" %}
```javascript
function sto_emplace(
    sto: ByteArray | HexString,
    field_bytes: ByteArray | HexString,
    field_id: number
  ): ErrorCode | ByteArray
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
uint8_t tx_out[1024];

int64_t tx_len =
    sto_emplace(tx_out, sizeof(tx_out),
                tx_in, tx_len,
                sequence_field, 5, sfSequence);

if (tx_len <= 0)
    rollback("Emplacing failed.", 17, 1);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
const tx_out = sto_emplace(tx_in, sequence_field, sfSequence)
if (typeof tx_out === 'number')
    rollback("Emplacing failed.", 1)
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}
| Name       | Type      | Description                                                                                                                                                             |
| ---------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| write\_ptr | uint32\_t | The buffer to write the modified STObject to                                                                                                                            |
| write\_len | uint32\_t | The length of the output buffer                                                                                                                                         |
| sread\_ptr | uint32\_t | The buffer to read the source STObject from                                                                                                                             |
| sread\_len | uint32\_t | The Length of the source object                                                                                                                                         |
| fread\_ptr | uint32\_t | The buffer to read the field to be emplaced/injected from                                                                                                               |
| fread\_len | uint32\_t | The length of the field to be emplaced/injected                                                                                                                         |
| field\_id  | uint32\_t | The `sf` code (location) to form the emplacement. If this already exists in the source object then the existing field is overriden. If it doesn't exist it is inserted. |


{% endtab %}

{% tab title="Javascript" %}


| Name         | Type                   | Description                                                                   |
| ------------ | ---------------------- | ----------------------------------------------------------------------------- |
| sto          | ByteArray \| HexString | The STO object (binary encoded ledger data) to which the field will be added. |
| field\_bytes | ByteArray \| HexString | The bytes representing the field to be added.                                 |
| field\_id    | number                 | The ID of the field to be added.                                              |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
<table><thead><tr><th width="169">Type</th><th>Description</th></tr></thead><tbody><tr><td>int64_t</td><td>The number of bytes written to <code>write_ptr</code><br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.<br><br><code>TOO_SMALL</code><br>- Output buffer must be at least as large as the source object + the injected field, even if the field is only being overriden.<br><br><code>TOO_BIG</code><br>- Field you are attempting to emplace is too large<br><br><code>PARSE_ERROR</code><br>- The supplied STObject is malformed or not an STObject.</td></tr></tbody></table>


{% endtab %}

{% tab title="Javascript" %}


<table><thead><tr><th width="169">Type</th><th>Description</th></tr></thead><tbody><tr><td>ErrorCode | ByteArray</td><td>The updated STO object in binary encoded ledger data format, or an error code if the operation fails.</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

