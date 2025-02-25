---
description: Retreive the 20 byte Account ID the Hook is executing on
---

# hook\_account

### Behaviour

{% tabs %}
{% tab title="C" %}
* Write the 20 byte Account ID to the write\_ptr
{% endtab %}

{% tab title="Javascript" %}
* Retrieve the 20 byte Account ID the Hook is executing on.
{% endtab %}
{% endtabs %}

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t hook_account (
    uint32_t write_ptr,
    uint32_t write_len
);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function hook_account(): ErrorCode | ByteArray
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
uint8_t hook_acc_id[20];
int64_t bytes_written = 
    hook_account(hook_acc_id, 20);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
hook_account()
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}
| Name       | Type      | Description                                                                              |
| ---------- | --------- | ---------------------------------------------------------------------------------------- |
| write\_ptr | uint32\_t | Pointer to a buffer of a suitable size to store the output. Should be at least 20 bytes. |
| write\_len | uint32\_t | Length of the output buffer.                                                             |
{% endtab %}

{% tab title="Javascript" %}
No parameters
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                            |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| int64\_t | <p>The number of bytes written<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.</p> |
{% endtab %}

{% tab title="Javascript" %}
| Type                   | Description                                                                               |
| ---------------------- | ----------------------------------------------------------------------------------------- |
| ErrorCode or ByteArray | Returns the Account ID the Hook is executing on, or an error code if the retrieval fails. |
{% endtab %}
{% endtabs %}

