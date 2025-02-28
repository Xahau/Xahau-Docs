---
description: Get the burden of a hypothetically emitted transaction
---

# etxn\_burden

### Concepts

* [Emitted Transactions](../../../concepts/emitted-transactions.md)

### Behaviour

* Return the burden an emitted transaction will carry.

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t etxn_burden (
    void
);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function etxn_burden(): ErrorCode | number
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t burden = etxn_burden();
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
const burden = etxn_burden()
```
{% endtab %}
{% endtabs %}



### Parameters

None

### Return Code

{% tabs %}
{% tab title="C" %}
<table><thead><tr><th width="165">Type</th><th>Description</th></tr></thead><tbody><tr><td>int64_t</td><td>The burden an emitted transaction will need in order to be successfully passed to <code>emit()</code></td></tr></tbody></table>
{% endtab %}

{% tab title="Javascript" %}
<table><thead><tr><th width="165">Type</th><th>Description</th></tr></thead><tbody><tr><td>number</td><td>An ErrorCode if there is an error, or the current burden value on success.</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

