---
description: Generate a 32 byte nonce for use in an emitted transaction
---

# etxn\_nonce

### Concepts

* [Emitted Transactions](../../../concepts/emitted-transactions.md)

### Behaviour

{% tabs %}
{% tab title="C" %}
* Write the 32 byte Hash to the write\_ptr
{% endtab %}

{% tab title="Javascript" %}
* Returns an ErrorCode if there is an error, or an array containing the nonce value on success.
{% endtab %}
{% endtabs %}



### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t etxn_nonce (
    uint32_t write_ptr,
    uint32_t write_len
);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
function etxn_nonce(): ErrorCode | ByteArray
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
uint8_t n[32];
int64_t bytes_written = 
    etxn_nonce(n, 32);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
const nonce = etxn_nonce()
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
No parameters
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
<table><thead><tr><th width="187">Type</th><th>Description</th></tr></thead><tbody><tr><td>int64_t</td><td>The number of bytes written<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.</td></tr></tbody></table>
{% endtab %}

{% tab title="Javascript" %}
<table><thead><tr><th width="187">Type</th><th>Description</th></tr></thead><tbody><tr><td>ErrorCode | ByteArray</td><td>Returns an ErrorCode if there is an error, or an array containing the nonce value on success.</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

