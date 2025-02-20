---
description: Fetch the last closed ledger's timestamp
---

# ledger\_last\_time

### Behaviour

* Return the Xahau Timestamp from the last closed ledger.

> ### 📘Tip
>
> Xahau timestamps are identical to a unix timestamps except that they are offset by `-946684800`.
>
> The equivalent unix timestamp is: `ledger_last_time() + 946684800;`

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t ledger_last_time ();
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
function ledger_last_time(): ErrorCode | number
```
{% endtab %}
{% endtabs %}

### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t ts =
    ledger_last_time();
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
ledger_last_time()
```
{% endtab %}
{% endtabs %}



### Parameters

This API takes no parameters.

### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                  |
| -------- | -------------------------------------------- |
| int64\_t | The XRPL timestamp of the last closed ledger |


{% endtab %}

{% tab title="Javascript" %}


| Type   | Description                                                                                          |
| ------ | ---------------------------------------------------------------------------------------------------- |
| number | Returns an error code if an error occurs, or a number representing the timestamp of the last ledger. |
{% endtab %}
{% endtabs %}

