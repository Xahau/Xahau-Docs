---
description: Generate a 32 byte nonce for use in an emitted transaction
---

# ledger\_nonce

### Behaviour

{% tabs %}
{% tab title="C" %}
* Write a 32 byte random value to the write\_ptr
{% endtab %}

{% tab title="Javascript" %}
* Retrieves the nonce of the current ledger.
{% endtab %}
{% endtabs %}



### Definition

C

{% tabs %}
{% tab title="C" %}
```c
int64_t ledger_nonce (
    uint32_t write_ptr,
    uint32_t write_len
);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
function ledger_nonce(): ErrorCode | ByteArray
```
{% endtab %}
{% endtabs %}

### Example

{% tabs %}
{% tab title="C" %}
```c
uint8_t n[32];
int64_t bytes_written = 
    ledger_nonce(n, 32);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
const nonce = ledger_nonce()
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


| Type                   | Description                                                                                                                           |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| ErrorCode \| ByteArray | Returns an error code if an error occurs, or an array representing the nonce of the current ledger. specified outside of hook memory. |
{% endtab %}

{% tab title="Javascript" %}


| Type     | Description                                                                                                                                            |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| int64\_t | <p>The number of bytes written<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.</p> |
{% endtab %}
{% endtabs %}

