---
description: Output the originating transaction in JSON format.
---

# otxn\_json

### Behaviour

{% tabs %}
{% tab title="Javascript" %}
* Output the originating transaction in JSON format.
* Returns the originating transaction as a JSON object or Transaction, or an ErrorCode if the retrieval fails.
{% endtab %}
{% endtabs %}

### Definition

{% tabs %}
{% tab title="Javascript" %}
```javascript
function otxn_json(): ErrorCode | Record<string, any> | Transaction
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="Javascript" %}
```javascript
otxn_json()
```
{% endtab %}
{% endtabs %}



### Parameters

No parameters

### Return Code

{% tabs %}
{% tab title="Javascript" %}
| Type                                             | Description                                                                                                  |
| ------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ |
| ErrorCode \| Record\<string, any> \| Transaction | Returns the originating transaction as a JSON object or Transaction, or an ErrorCode if the retrieval fails. |
{% endtab %}
{% endtabs %}

