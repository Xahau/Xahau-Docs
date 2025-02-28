---
description: >-
  Parse the STI_AMOUNT in the specified slot and return it as an XFL enclosed
  number
---

# slot\_float

### Behaviour

{% tabs %}
{% tab title="C" %}
* Parse the STI\_AMOUNT in the specified slot and return it as an XFL enclosed number
{% endtab %}

{% tab title="Javascript" %}
* Retrieves the bigint value associated with the specified slot.
* Returns an error code or the bigint value.
{% endtab %}
{% endtabs %}

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t slot_float (
    uint32_t slot_no
);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function slot_float(slotno: number): ErrorCode | bigint
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t xfl =
  	slot_float(amt_slot);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
const xfl = slot_float(amt_slot)
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
| Name   | Type   | Description                                        |
| ------ | ------ | -------------------------------------------------- |
| slotno | number | The slot number to retrieve the bigint value from. |
{% endtab %}
{% endtabs %}

### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                                                                                                                                                          |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| int64\_t | <p>The XFL enclosing number<br><br>If negative, an error:<br><code>DOESNT_EXIST</code><br>- the specified slot does not contain any object or it is an invalid slot<br><br><code>NOT_AN_AMOUNT</code><br>- the specified slot does not contain an <code>STI_AMOUNT</code> object</p> |
{% endtab %}

{% tab title="Javascript" %}
| Type                | Description                                |
| ------------------- | ------------------------------------------ |
| bigint or ErrorCode | Returns an error code or the bigint value. |
{% endtab %}
{% endtabs %}

