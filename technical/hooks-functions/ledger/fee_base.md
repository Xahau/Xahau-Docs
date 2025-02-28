---
description: Fetch the fee base of the current ledger
---

# fee\_base

### Concepts

* [Hook Fees](../../../concepts/hook-fees.md)

### Behaviour

* Return the fee base from the current ledger

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t fee_base();
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function fee_base(): number
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t fee =
    fee_base();
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
const fee = fee_base()
```
{% endtab %}
{% endtabs %}



### Parameters

This API takes no parameters.

### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                        |
| -------- | ---------------------------------- |
| int64\_t | The fee base of the current ledger |
{% endtab %}

{% tab title="Javascript" %}


| Type   | Description                        |
| ------ | ---------------------------------- |
| number | The fee base of the current ledger |
{% endtab %}
{% endtabs %}

