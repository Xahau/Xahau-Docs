---
description: Retrieve the parameter value for a named hook parameter
---

# hook\_param

### Behaviour

{% tabs %}
{% tab title="C" %}
* Look up the value for a named parameter specified in `read_ptr`
* Write the parameter's value to `write_ptr`
{% endtab %}

{% tab title="Javascript" %}
* Retrieve the value of a parameter associated with the specified key.
* Returns the value associated with the key, or an error code if the retrieval fails.
{% endtab %}
{% endtabs %}

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t hook_param (
    uint32_t write_ptr,
    uint32_t write_len,
    uint32_t read_ptr,
    uint32_t read_len
);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function hook_param(key: ByteArray | HexString): ErrorCode | ByteArray
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
uint8_t pname[] = {0xCAU, 0xFEU};
uint8_t pvalue[32];
int64_t value_len = 
    hook_param(pvalue, 32, pname, 2);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
hook_param(key)
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}
| Name       | Type      | Description                                                                              |
| ---------- | --------- | ---------------------------------------------------------------------------------------- |
| write\_ptr | uint32\_t | Pointer to a buffer of a suitable size to store the output. Should be at least 32 bytes. |
| write\_len | uint32\_t | Length of the output buffer.                                                             |
| read\_ptr  | uint32\_t | Pointer to a buffer containing the parameter's name                                      |
| read\_len  | uint32\_t | Length of the parameter's name                                                           |


{% endtab %}

{% tab title="Javascript" %}


| Name | Type                   | Description                                        |
| ---- | ---------------------- | -------------------------------------------------- |
| key  | ByteArray or HexString | The key for which to retrieve the parameter value. |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                                                                                                                                                                                                                                                                    |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The number of bytes written<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.<br><br><code>DOESNT_EXIST</code><br>- The specified paramater doesn't exist or is null<br><br><code>TOO_SMALL</code><br>- The parameter name can't be null<br><br><code>TOO_BIG</code><br>- The parameter name is greater than 32 bytes</p> |


{% endtab %}

{% tab title="Javascript" %}


| Type                   | Description                                                                         |
| ---------------------- | ----------------------------------------------------------------------------------- |
| ByteArray or ErrorCode | Returns the value associated with the key, or an error code if the retrieval fails. |
{% endtab %}
{% endtabs %}

