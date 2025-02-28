---
description: Get the burden of the originating transaction
---

# otxn\_burden

### Behaviour

{% tabs %}
{% tab title="C" %}
* Return the burden of the originating transaction or `1` if no burden field is present.
{% endtab %}

{% tab title="Javascript" %}
* Retrieve the burden of the originating transaction.
* Returns the burden as a number, or an ErrorCode if the retrieval fails.
{% endtab %}
{% endtabs %}

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t otxn_burden (
    void
);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function otxn_burden(): ErrorCode | number
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t burden = 
  otxn_burden();
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
const burden = otxn_burden()
```
{% endtab %}
{% endtabs %}



### Parameters

None

### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                |
| -------- | ---------------------------------------------------------------------------------------------------------- |
| int64\_t | The burden of the originating transaction, or `1` if no burden was present on the originating transaction. |
{% endtab %}

{% tab title="Javascript" %}
| Type                | Description                                                             |
| ------------------- | ----------------------------------------------------------------------- |
| number or ErrorCode | Returns the burden as a number, or an ErrorCode if the retrieval fails. |
{% endtab %}
{% endtabs %}

