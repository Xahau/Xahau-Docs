---
description: Load the originating transaction into a slot
---

# otxn\_slot

### Behaviour

* Emplace the originating transaction into the slot specified or into a new slot if no slot is specified

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t otxn_slot (
  	uint32_t slot_no
);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function otxn_slot(slotno: number): ErrorCode | ByteArray
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t otxn_slot_no = 
		otxn_slot(0);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
otxn_slot(slotno)
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}
| Name     | Type      | Description                                                                   |
| -------- | --------- | ----------------------------------------------------------------------------- |
| slot\_no | uint32\_t | The slot number to emplace into, or 0 if you wish to pick the next available. |
{% endtab %}

{% tab title="Javascript" %}
| Name   | Type   | Description                 |
| ------ | ------ | --------------------------- |
| slotno | number | The slot number to look up. |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                                                                                                                                                                        |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The slot the otxn was placed in<br><br><code>INVALID_ARGUMENT</code><br>- specified slot number exceeds the largest possible slot number<br><br><code>NO_FREE_SLOTS</code><br>- the request could not granted because no free slot was avaialble to place the originating transaction into.</p> |
{% endtab %}

{% tab title="Javascript" %}
| Type                   | Description                                                                                                                            |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| ErrorCode \| ByteArray | <p></p><p>Returns the value associated with the specified slot number as an array of numbers, or an ErrorCode if the lookup fails.</p> |
{% endtab %}
{% endtabs %}

