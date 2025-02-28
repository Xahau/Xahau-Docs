---
description: >-
  Index into a xahaud serialized array and return the location and length of an
  index
---

# sto\_subarray

### Concepts

* [Serialized Objects](../../../concepts/serialized-objects.md)

### Behaviour

{% tabs %}
{% tab title="C" %}
* Parse a STArray pointed to by `read_ptr`
* Find the array index specified by `array_id`
* Return the byte offset and length of the serialized field within the STObject, if it is found

> ### 🚧Field ID encoding
>
> The `sto_` apis accept a `field_id` parameter encoded as follows: `(type << 16U) + field`\
> Thus type 1 field 2 would be `0x10002U`.
>
> In the case of this array field ID is `array_id`.
{% endtab %}

{% tab title="Javascript" %}
* Ask for the STO object (binary encoded ledger data) from which to extract the subarray.
* Find the array index specified by `array_id`
* Return a subarray from an STO object.
{% endtab %}
{% endtabs %}

### Definition

C

{% tabs %}
{% tab title="C" %}
<pre class="language-c"><code class="lang-c"><strong>int64_t sto_subarray (
</strong>    uint32_t read_ptr,
<strong>    uint32_t read_len,
</strong>    uint32_t array_id
);
</code></pre>


{% endtab %}

{% tab title="Javascript" %}
```javascript
function sto_subarray(
    sto: ByteArray | HexString,
    array_id: number
  ): bigint | number
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
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
{% endtab %}

{% tab title="Javascript" %}
```javascript
const SUB_OFFSET = (x) => Number(x >> 32n)
const SUB_LENGTH = (x) => Number(x & 0xFFFFFFFFn)

const memo_lookup = sto_subarray(memos, 0)

if (typeof memo_lookup === 'number')
{
    // sfMemo was not found in the STObject pointed at
}
else
{
    // 0th index of the STArray was found and its location is as follows:
    const memo_start = SUB_OFFSET(memo_lookup)
    const memo_len = SUB_LENGTH(memo_lookup)
    const memo = memos.slice(memo_start, memo_len)
}
```
{% endtab %}
{% endtabs %}

### Parameters

{% tabs %}
{% tab title="C" %}
| Name      | Type      | Description                                                               |
| --------- | --------- | ------------------------------------------------------------------------- |
| read\_ptr | uint32\_t | Pointer to the buffer containing the STArray                              |
| read\_len | uint32\_t | Length of STArray                                                         |
| array\_id | uint32\_t | The index of the entry within the STArray you are seeking. Starts from 0. |


{% endtab %}

{% tab title="Javascript" %}


| Name      | Type                   | Description                                                                     |
| --------- | ---------------------- | ------------------------------------------------------------------------------- |
| sto       | ByteArray \| HexString | The STO object (binary encoded ledger data) from which to extract the subarray. |
| array\_id | number                 | The ID of the array to be extracted.                                            |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The location of the field within the specified buffer:<br>- The high 32 bits are the offset location.<br>- The low 32 bits are the length.<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.<br><br><code>TOO_SMALL</code><br>- Input buffer isn't large enough to possibly contain a valid STArray.<br><br><code>DOESNT_EXIST</code><br>- The searched for index isn't present in the supplied STArray.<br><br><code>PARSE_ERROR</code><br>- The supplied STArray is malformed or not an STArray.</p> |


{% endtab %}

{% tab title="Javascript" %}


| Type               | Description                                                                                                                                                                                        |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| bigint / ErrorCode | <p>The location of the field within the specified buffer:<br>- The high 32 bits are the offset location.<br>- The low 32 bits are the length.<br><br>or an error code if the extraction fails.</p> |
{% endtab %}
{% endtabs %}

