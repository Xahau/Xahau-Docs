---
description: Get the generation of a hypothetically emitted transaction
---

# etxn\_generation

### Concepts

* [Emitted Transactions](../../../concepts/emitted-transactions.md)

### Behaviour

* Return the generation an emitted transaction will carry.

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t etxn_generation (
    void
);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
function etxn_generation(): ErrorCode | number
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t burden = 
  etxn_generation();
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
etxn_generation();
```
{% endtab %}
{% endtabs %}



### Parameters

None

### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                    |
| -------- | ---------------------------------------------------------------------------------------------- |
| int64\_t | The generation an emitted transaction will need in order to be successfully passed to `emit()` |


{% endtab %}

{% tab title="Javascript" %}


| Type   | Description                                                                                         |
| ------ | --------------------------------------------------------------------------------------------------- |
| number | Returns An ErrorCode if there is an error, or a number indicating the generation result on success. |
{% endtab %}
{% endtabs %}

