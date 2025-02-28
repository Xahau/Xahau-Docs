---
description: Compute the serialized size of an object in a slot
---

# slot\_size

### Behaviour

{% tabs %}
{% tab title="C" %}
* Return the number of bytes the object in the specified slot occupies when serialized
{% endtab %}

{% tab title="Javascript" %}
* Retrieves the size of the specified slot.
{% endtab %}
{% endtabs %}

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t slot_size (
    uint32_t slot_no
);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function slot_size(slotno: number): ErrorCode | number
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t bytes_needed = slot_size(1); // get size of slot 1
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
const bytes_needed = slot_size(1); // get size of slot 1
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
| Name   | Type   | Description                           |
| ------ | ------ | ------------------------------------- |
| slotno | number | The slot number to check the size of. |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                                                                            |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| int64\_t | <p>The number of bytes the object occupies when serialized<br><br>If negative, an error:<br><code>DOESNT_EXIST</code><br>- the specified slot does not contain any object or it is an invalid slot</p> |
{% endtab %}

{% tab title="Javascript" %}
| Type                | Description                                    |
| ------------------- | ---------------------------------------------- |
| ErrorCode \| number | Returns an error code or the size of the slot. |
{% endtab %}
{% endtabs %}

