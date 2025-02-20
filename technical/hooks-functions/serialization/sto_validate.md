---
description: Validate an STObject
---

# sto\_validate

### Concepts

* [Serialized Objects](../../../concepts/serialized-objects.md)

### Behaviour

{% tabs %}
{% tab title="C" %}
* Parse an STObject pointed to by `read_ptr`
* Return 1 if the serialization is valid, 0 otherwise.
{% endtab %}

{% tab title="Javascript" %}
* The `blob` (e.g. serialized transaction) is provided to be validated.
* Returns number 1 if the STObject is valid, 0 if it isn't, or an error code if validation fails.
{% endtab %}
{% endtabs %}



### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t sto_validate (
    uint32_t read_ptr,
    uint32_t read_len
);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
function sto_validate(blob: ByteArray | HexString): ErrorCode | number
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t result = 
  sto_validate(tx_out, sizeof(tx_out));

if (tx_len <= 0)
    rollback("Invalid STO.", 12, 1);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
sto_validate(blob)
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}
| Name      | Type      | Description                                 |
| --------- | --------- | ------------------------------------------- |
| read\_ptr | uint32\_t | The buffer to read the source STObject from |
| read\_len | uint32\_t | The Length of the source object             |


{% endtab %}

{% tab title="Javascript" %}


| Name | Type                   | Description                                             |
| ---- | ---------------------- | ------------------------------------------------------- |
| blob | ByteArray \| HexString | The blob (e.g. serialized transaction) to be validated. |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                                                                                                                       |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p><code>1</code> if the STObject pointed to by <code>read_ptr</code> is a valid STObject.<br><code>0</code> if it isn't.<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.</p> |


{% endtab %}

{% tab title="Javascript" %}
| Type                | Description                                                                                     |
| ------------------- | ----------------------------------------------------------------------------------------------- |
| ErrorCode \| number | Returns number 1 if the STObject is valid, 0 if it isn't, or an error code if validation fails. |
{% endtab %}
{% endtabs %}

