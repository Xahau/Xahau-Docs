---
description: Output the canonical hash of the originating transaction
---

# otxn\_id

### Behaviour

{% tabs %}
{% tab title="C" %}
* Write the canonical hash of the originating transaction to the output buffer.
* If flags = 1 and the transaction is an EMIT\_FAILURE transaction then write the canonical hash of the originating transaction that caused the emission.
{% endtab %}

{% tab title="Javascript" %}
* Output the canonical hash of the originating transaction.
* Returns the transaction hash as an array of numbers, or an ErrorCode if the retrieval fails.
{% endtab %}
{% endtabs %}

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t otxn_id (
    uint32_t write_ptr,
    uint32_t write_len,
    uint32_t flags
);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function otxn_id(flag: number): ErrorCode | ByteArray
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
uint8_t txn_id[32];
int64_t bytes_written = 
    otxn_id(txn_id, 32, 0);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
const tx_id = otxn_id(0)
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}
| Name       | Type      | Description                                                                                                                                                                                                                 |
| ---------- | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| write\_ptr | uint32\_t | Pointer to a buffer of to store the hash.                                                                                                                                                                                   |
| write\_len | uint32\_t | Length of the output buffer. Should be at least 32 bytes.                                                                                                                                                                   |
| flags      | uint32\_t | <p>If <code>0</code>:<br>Write the canonical hash of the originating transaction.<br><br>If <code>1</code> AND the originating transaction is an EMIT_FAILURE:<br>Write the canonical hash of the emitting transaction.</p> |
{% endtab %}

{% tab title="Javascript" %}
| Name  | Type   | Description                                                                                                                                                                                                                 |
| ----- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| flags | number | <p>If <code>0</code>:<br>Write the canonical hash of the originating transaction.<br><br>If <code>1</code> AND the originating transaction is an EMIT_FAILURE:<br>Write the canonical hash of the emitting transaction.</p> |
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
| Type                   | Description                                                                                  |
| ---------------------- | -------------------------------------------------------------------------------------------- |
| ErrorCode \| ByteArray | Returns the transaction hash as an array of numbers, or an ErrorCode if the retrieval fails. |
{% endtab %}
{% endtabs %}

