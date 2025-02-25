---
description: Count the elements of an array object in a slot
---

# slot\_count

### Behaviour

* Count the elements of an array in the specified slot
* Return the count

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t slot_count (
    uint32_t slot_no
);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
function slot_count(slotno: number): ErrorCode | number
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
slot_count(1); // assumes an array is slotted into slot=1
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
slot_count(slotno)
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
| Type     | Description                                                                                                                                                                                                                                                                              |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The number of elements inside the slotted array<br><br>If negative, an error:<br><code>DOESNT_EXIST</code><br>- the specified slot does not contain any object or it is an invalid slot<br><br><code>NOT_AN_ARRAY</code><br>- the specified slot does not contain an array object</p> |
{% endtab %}

{% tab title="Javascript" %}
| Type                | Description                                    |
| ------------------- | ---------------------------------------------- |
| ErrorCode or number | Returns an error code or the count of entries. |
{% endtab %}
{% endtabs %}

