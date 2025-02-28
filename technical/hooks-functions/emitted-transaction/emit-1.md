---
description: Emit a new transaction from the hook
---

# emit

### Concepts

* [Emitted Transactions](../../../concepts/emitted-transactions.md)

### Behaviour

{% tabs %}
{% tab title="C" %}
* Read a transaction from `read_ptr`
* Validate the transaction against the emission rules
* Emit the transaction into consensus when valid
* Write canonical transaction hash to `write_ptr`
{% endtab %}

{% tab title="Javascript" %}
* This function emits the provided transaction JSON.
* On success, it returns the number of emitted transaction hashes.&#x20;
* If there is an error, it returns an error code.
{% endtab %}
{% endtabs %}

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t emit (
    uint32_t write_ptr,
    uint32_t write_len,
    uint32_t read_ptr,
    uint32_t read_len
);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
function emit(
    txJson: Record<string, any> | Transaction
  ): ErrorCode | ByteArray
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
if (emit(tx, tx_len) < 0)
    rollback("Failed to emit!", 15, 1);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
const emitResult = emit(txJson)
if(typeof emitResult === 'number')
    rollback("Failed to emit!", 1)
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}
<table><thead><tr><th>Name</th><th width="124">Type</th><th>Description</th></tr></thead><tbody><tr><td>write_ptr</td><td>uint32_t</td><td>Pointer to a buffer to write the transaction hash to</td></tr><tr><td>write_len</td><td>uint32_t</td><td>The size of the buffer to write the transaction hash to (should be 32.)</td></tr><tr><td>read_ptr</td><td>uint32_t</td><td>Pointer to the transaction to emit</td></tr><tr><td>read_len</td><td>uint32_t</td><td>The length of the transaction</td></tr></tbody></table>


{% endtab %}

{% tab title="Javascript" %}


<table><thead><tr><th>Name</th><th width="124">Type</th><th>Description</th></tr></thead><tbody><tr><td>txJson</td><td>Record&#x3C;string, any> | Transaction</td><td>The TX JSON to emit.</td></tr></tbody></table>
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
<table><thead><tr><th width="127">Type</th><th>Description</th></tr></thead><tbody><tr><td>int64_t</td><td>On success, the number of bytes of transaction hash written (32), or:<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.<br><br><code>PREREQUISITE_NOT_MET</code><br>- <code>emit_reserve</code> must be called first<br><br><code>TOO_MANY_EMITTED_TXN</code><br>- the number of emitted transactions is now greater than the promise made when <code>emit_reserve</code> was called earlier<br><br><code>EMISSION_FAILURE</code><br>- the transaction was malformed according to the emission rules.</td></tr></tbody></table>


{% endtab %}

{% tab title="Javascript" %}


<table><thead><tr><th width="231">Type</th><th>Description</th></tr></thead><tbody><tr><td>ErrorCode | ByteArray</td><td>Returns an ErrorCode if there is an error, or an array of emitted transaction hashes on success.</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

