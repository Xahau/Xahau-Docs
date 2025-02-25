---
description: Retrieve the parameter value for a named Invoke transaction parameter
---

# otxn\_param

### Behaviour

{% tabs %}
{% tab title="C" %}
* Look up the value for a named parameter specified in `read_ptr` on the originating transaction (ttINVOKE only).
* Write the parameter's value to `write_ptr`
{% endtab %}

{% tab title="Javascript" %}
* Look up the value for a named parameter specified on the originating transaction.
* Returns the value of the specified parameter, or an ErrorCode if the lookup fails.
{% endtab %}
{% endtabs %}

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t otxn_param (
    uint32_t write_ptr,
    uint32_t write_len,
    uint32_t read_ptr,
    uint32_t read_len
);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function otxn_param(name: ByteArray | HexString): ErrorCode | ByteArray
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
    otxn_param(pvalue, 32, pname, 2);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
otxn_param(name)
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
| Name | Type                   | Description                                                               |
| ---- | ---------------------- | ------------------------------------------------------------------------- |
| name | ByteArray \| HexString | The name of the parameter to look up, specified as a ByteArray or string. |
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
| Type                   | Description                                                                        |
| ---------------------- | ---------------------------------------------------------------------------------- |
| ErrorCode \| ByteArray | Returns the value of the specified parameter, or an ErrorCode if the lookup fails. |
{% endtab %}
{% endtabs %}

