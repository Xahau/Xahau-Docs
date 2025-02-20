---
description: Format JSON as an STO object (binary encoded ledger data).
---

# sto\_from\_json

### Concepts

* [Serialized Objects](../../../concepts/serialized-objects.md)

### Behaviour

{% tabs %}
{% tab title="Javascript" %}
* Takes a JSON object and converts it into a binary encoded ledger data format.
* Returns STO Object in binary encoded ledger data format, or an error code if the conversion fails.
{% endtab %}
{% endtabs %}



### Definition

{% tabs %}
{% tab title="Javascript" %}
```javascript
function sto_from_json(
    jsonobj: Record<string, any> | Transaction
  ): ErrorCode | ByteArray
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="Javascript" %}
```javascript
sto_from_json(jsonobj)
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="Javascript" %}


| Name    | Type                                | Description                                     |
| ------- | ----------------------------------- | ----------------------------------------------- |
| jsonobj | Record\<string, any> \| Transaction | JSON object to be converted into an STO object. |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="Javascript" %}


| Type                   | Description                                                                                |
| ---------------------- | ------------------------------------------------------------------------------------------ |
| ErrorCode \| ByteArray | STO Object in binary encoded ledger data format, or an error code if the conversion fails. |
{% endtab %}
{% endtabs %}

