# etxn\_fee\_base

> ### 🚧 Warning
>
> Fees on a Hooks-enabled ledger are non trivial. See: [Hook Fees](../../../concepts/hook-fees.md) for details.

### Concepts

* [Emitted Transactions](../../../concepts/emitted-transactions.md)

### Behaviour

* Return the amount of the fee in drops recommended for a to-be emitted transaction.

### Definition

C

{% tabs %}
{% tab title="C" %}
```c
int64_t etxn_fee_base (
    uint32_t read_ptr,
  	uint32_t read_len
);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
function etxn_fee_base(txblob: ByteArray | HexString): ErrorCode | number
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t fee_to_pay =
    etxn_fee_base(tx_blob, tx_blob_len);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
etxn_fee_base(txblob)
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}
<table><thead><tr><th>Name</th><th width="118">Type</th><th>Description</th></tr></thead><tbody><tr><td>read_ptr</td><td>uint32_t</td><td>Pointer to the buffer containing the serialized transaction you intend to emit. The fee field is required but ignored (you may use zero). Use the output of this function to populate the fee field correctly.</td></tr><tr><td>read_len</td><td>uint32_t</td><td>The length of the tx blob.</td></tr></tbody></table>


{% endtab %}

{% tab title="Javascript" %}


<table><thead><tr><th>Name</th><th width="118">Type</th><th>Description</th></tr></thead><tbody><tr><td>txblob</td><td>ByteArray | HexString</td><td>The transaction blob, which can be an array of numbers or a string.</td></tr></tbody></table>
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}


| Type     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The smallest number of drops that an emitted txn would need to be accepted.<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- The provided buffer is not validly within the hook memory.<br><br><code>PREREQUISITE_NOT_MET</code><br>- <code>etxn_reserve</code> has not been called first.<br><br><code>INVALID_TXN</code><br>- The provided buffer did not contain a valid serialized transaction. (Deserialization failed, or a required field was missing.)</p> |
{% endtab %}

{% tab title="Javascript" %}


| Type   | Description                                                               |
| ------ | ------------------------------------------------------------------------- |
| number | An ErrorCode if there is an error, or the calculated base fee on success. |
{% endtab %}
{% endtabs %}

