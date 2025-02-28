---
description: Free up a currently occupied slot
---

# slot\_clear

### Behaviour

* Free the specified slot, releasing any object that was slotted there

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t slot_clear (
    uint32_t slot_no
);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function slot_clear(slotno: number): ErrorCode | number
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
slot_clear(1); // assumes a transaction is slotted into slot=1
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
slot_clear(1) // assumes a transaction is slotted into slot=1
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}
| Name     | Type      | Description     |
| -------- | --------- | --------------- |
| slot\_no | uint32\_t | The slot number |
{% endtab %}

{% tab title="Javascript" %}
| Name   | Type   | Description     |
| ------ | ------ | --------------- |
| slotno | number | The slot number |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                                               |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p><code>1</code> or an error<br><br>If negative, an error:<br><code>DOESNT_EXIST</code><br>- the specified slot does not contain any object or it is an invalid slot</p> |
{% endtab %}

{% tab title="Javascript" %}
| Type                | Description                                                 |
| ------------------- | ----------------------------------------------------------- |
| ErrorCode \| number | Returns an error code or the result of the clear operation. |
{% endtab %}
{% endtabs %}

