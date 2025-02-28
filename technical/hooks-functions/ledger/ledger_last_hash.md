---
description: Retreive the 32 byte namespace biased SHA512H of the last closed ledger
---

# ledger\_last\_hash

### Behaviour

{% tabs %}
{% tab title="C" %}
* Write the 32 byte Hash to the write\_ptr
{% endtab %}

{% tab title="Javascript" %}
* Retrieves the hash of the last ledger.
{% endtab %}
{% endtabs %}

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t ledger_last_hash (
    uint32_t write_ptr,
    uint32_t write_len
);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
function ledger_last_hash(): ErrorCode | ByteArray
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
uint8_t hash[32];
int64_t bytes_written = 
    ledger_last_hash(hash, 32);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
const hash = ledger_last_hash()
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


{% endtab %}

{% tab title="Javascript" %}

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
| Type   | Description                                                                                     |
| ------ | ----------------------------------------------------------------------------------------------- |
| number | Returns an error code if an error occurs, or an array representing the hash of the last ledger. |
{% endtab %}
{% endtabs %}

