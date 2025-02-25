---
description: Retreive the 32 byte namespace biased SHA512H of the currently executing Hook
---

# hook\_hash

### Behaviour

{% tabs %}
{% tab title="C" %}
* Look up the hash of the hook installed on hook account at position `hook_no`
* Write the 32 byte hash to `write_ptr`
{% endtab %}

{% tab title="Javascript" %}
* Look up the hash of the hook installed on the hook account at the specified position.
* The Namespace biased SHA512H of the currently executing Hook, or an error code if the lookup fails.
{% endtab %}
{% endtabs %}



### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t hook_hash (
    uint32_t write_ptr,
    uint32_t write_len,
  	int32_t  hook_no
);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
function hook_hash(hookno: number): ErrorCode | ByteArray
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
uint8_t hash[32];
int64_t bytes_written = 
    hook_hash(hash, 32, -1);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
hook_hash(hookno)
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}
| Name       | Type      | Description                                                                                    |
| ---------- | --------- | ---------------------------------------------------------------------------------------------- |
| write\_ptr | uint32\_t | Pointer to a buffer of a suitable size to store the output. Should be at least 32 bytes.       |
| write\_len | uint32\_t | Length of the output buffer.                                                                   |
| hook\_no   | int32\_t  | The position in the hook chain the hook is located at, or -1 for the currently executing hook. |


{% endtab %}

{% tab title="Javascript" %}


| Name     | Type   | Description                                                                                    |
| -------- | ------ | ---------------------------------------------------------------------------------------------- |
| hook\_no | number | The position in the hook chain the hook is located at, or -1 for the currently executing hook. |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                                                                                                                                      |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The number of bytes written<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.<br><br><code>DOESNT_EXIST</code><br>- The specified hook sequence number doesn't exist in the hook chain.</p> |
{% endtab %}

{% tab title="Javascript" %}
| Type                   | Description                                                                                                 |
| ---------------------- | ----------------------------------------------------------------------------------------------------------- |
| ByteArray or ErrorCode | Returns the Namespace biased SHA512H of the currently executing Hook, or an error code if the lookup fails. |
{% endtab %}
{% endtabs %}

