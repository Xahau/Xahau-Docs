---
description: Format an STO object (binary encoded ledger data) as JSON format.
---

# sto\_to\_json

### Concepts

* [Serialized Objects](../../../concepts/serialized-objects.md)

### Behaviour

{% tabs %}
{% tab title="Javascript" %}
*   Format an STO object (binary encoded ledger data) as JSON format.&#x20;

    This function takes a serialized transaction `blob` and converts it into a human-readable JSON format.
* Returns Decoded JSON representation of the STO object, or an error code if the conversion fails.
{% endtab %}
{% endtabs %}



### Definition

{% tabs %}
{% tab title="Javascript" %}
```javascript
function sto_to_json(
    blob: ByteArray | HexString
  ): ErrorCode | Record<string, any> | Transaction
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="Javascript" %}
```javascript
sto_to_json(blob)
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="Javascript" %}


| Name | Type                   | Description                                             |
| ---- | ---------------------- | ------------------------------------------------------- |
| blob | ByteArray \| HexString | The blob (e.g. serialized transaction) to be converted. |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="Javascript" %}


| Type                                             | Description                                                                              |
| ------------------------------------------------ | ---------------------------------------------------------------------------------------- |
| ErrorCode \| Record\<string, any> \| Transaction | Decoded JSON representation of the STO object, or an error code if the conversion fails. |
{% endtab %}
{% endtabs %}

