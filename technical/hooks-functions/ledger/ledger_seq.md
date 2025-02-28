---
description: Fetch the current ledger sequence number
---

# ledger\_seq

### Behaviour

* Return the sequence number from the current ledger

### Definition

C

{% tabs %}
{% tab title="C" %}
```c
int64_t ledger_seq();
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function ledger_seq(): ErrorCode | number
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t seq =
    ledger_seq();
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
const seq = ledger_seq()
```
{% endtab %}
{% endtabs %}



### Parameters

This API takes no parameters.

### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                               |
| -------- | ----------------------------------------- |
| int64\_t | The sequence number of the current ledger |


{% endtab %}

{% tab title="Javascript" %}
| Type   | Description                               |
| ------ | ----------------------------------------- |
| number | The sequence number of the current ledger |
{% endtab %}
{% endtabs %}

