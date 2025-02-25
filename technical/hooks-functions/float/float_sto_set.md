---
description: Read a serialized amount into an XFL
---

# float\_sto\_set

### Concepts

* [Floating Point Numbers (XFL)](../../../concepts/floating-point-numbers-xfl.md)
* [Serialized Objects](../../../concepts/serialized-objects.md)

### Behaviour

{% tabs %}
{% tab title="C" %}
* Read a serialized floating point number.
* If there are more fields/data after the serialized floating pointer number then ignore them.
* Return it as an XFL enclosing number
{% endtab %}

{% tab title="Javascript" %}
* Sets the buffer for storing float representations.
* Returns ErrorCode or the result as a number.
{% endtab %}
{% endtabs %}



### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t float_sto_set (
    uint32_t read_ptr,
    uint32_t read_len
);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function float_sto_set(buf: ByteArray | HexString): ErrorCode | number

```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t vault_pusd = float_sto_set(vault, 8);
if (vault_pusd < 0)
  rollback("Failed to parse serialized float.", 33, 1);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
float_sto_set(buf)
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}
| Name      | Type      | Description                                                       |
| --------- | --------- | ----------------------------------------------------------------- |
| read\_ptr | uint32\_t | Pointer to a buffer contianing the serialized XFL. _May be null._ |
| read\_len | uint32\_t | The length of the buffer.                                         |


{% endtab %}

{% tab title="Javascript" %}
| Name | Type                   | Description        |
| ---- | ---------------------- | ------------------ |
| buf  | ByteArray \| HexString | The buffer to set. |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                                                                                                                                                                      |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| int64\_t | <p>The number of bytes written to the output buffer.<br><br>If negative, an error:<br><code>NOT_AN_OBJECT</code><br>- the supplied buffer did not contain a valid serialized floating point number<br><br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.</p> |
{% endtab %}

{% tab title="Javascript" %}
| Type                | Description                              |
| ------------------- | ---------------------------------------- |
| ErrorCode or number | An error code or the result as a number. |
{% endtab %}
{% endtabs %}

