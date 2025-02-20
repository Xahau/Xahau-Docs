---
description: Estimate the required fee for a txn to be emitted successfully
---

# etxn\_reserve

### Concepts

* [Emitted Transactions](../../../concepts/emitted-transactions.md)

### Behaviour

* Specifies a number of emitted transactions this hook might emit during execution.

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t etxn_fee_base (
    uint32_t count
);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
function etxn_reserve(txCount: number): ErrorCode | number
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t result = 
    etxn_fee_base(2);
if (result < 2)
    rollback("Error reserving!", 16, 1);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
etxn_fee_base(2);
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}
| Name  | Type      | Description                                                                                 |
| ----- | --------- | ------------------------------------------------------------------------------------------- |
| count | uint32\_t | The largest number of transactions this hook might emit during the course of one execution. |


{% endtab %}

{% tab title="Javascript" %}


| Name  | Type   | Description                                                      |
| ----- | ------ | ---------------------------------------------------------------- |
| count | number | The maximum amount of transactions this Hook is allowed to emit. |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                                                                                                                                                                                                                                            |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The maximum number of emitted transactions this hook may emit. This will always be the same as the <code>count</code> parameter or an error as below.<br><br>If negative, an error:<br><code>ALREADY_SET</code><br>- The hook already called this function earlier.<br><br><code>TOO_BIG</code><br>- The specified number of emitted transactions is too large.</p> |


{% endtab %}

{% tab title="Javascript" %}


| Type   | Description                                                                        |
| ------ | ---------------------------------------------------------------------------------- |
| number | An ErrorCode if there is an error, or the configured transaction count on success. |
{% endtab %}
{% endtabs %}

