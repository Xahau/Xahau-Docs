---
description: Serialize and output a slotted object
---

# slot

### Behaviour

{% tabs %}
{% tab title="C" %}
* Serialize the object currently occupying the specified slot
* Write the serialized version of the object to the output buffer

> ### 👍 Alternative use
>
> For small objects you may avoid using a buffer. Specify `0, 0` for `write_ptr, write_len` to attempt to return the slotted object as big endian packed data in the `int64_t` return code. Up to 63 bits of data may be returned this way.
{% endtab %}

{% tab title="Javascript" %}
* Retrieves the JSON Retrieves the data associated with the specified slot. of the specified slot.
* Returns an error code or the slot's data.
{% endtab %}
{% endtabs %}

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t slot (
    uint32_t write_ptr,
    uint32_t write_len,
    uint32_t slot_no
);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
function slot(slotno: number): ErrorCode | ByteArray
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
uint8_t txn[512];
int64_t bytes_written = 
    slot(txn, 512, 1); // assumes a transaction is slotted into slot=1
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
const txn = slot(1) // assumes a transaction is slotted into slot=1
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}
| Name       | Type      | Description                                                 |
| ---------- | --------- | ----------------------------------------------------------- |
| write\_ptr | uint32\_t | Pointer to a buffer of a suitable size to store the output. |
| write\_len | uint32\_t | Length of the output buffer.                                |
| slot\_no   | uint32\_t | The slot number                                             |
{% endtab %}

{% tab title="Javascript" %}
| Name   | Type   | Description     |
| ------ | ------ | --------------- |
| slotno | number | The slot number |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                                                                                                                                |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The number of bytes written<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.<br><br><code>TOO_SMALL</code><br>- output buffer was not large enough to hold the serialized object</p> |
{% endtab %}

{% tab title="Javascript" %}
| Type                   | Description                               |
| ---------------------- | ----------------------------------------- |
| ErrorCode \| ByteArray | Returns an error code or the slot's data. |
{% endtab %}
{% endtabs %}

