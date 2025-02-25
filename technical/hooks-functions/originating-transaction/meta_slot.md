---
description: Load the metadata of the originating transaction into a slot
---

# meta\_slot

### Behaviour

* If the Hook is being [Weakly Executed](../../../concepts/weak-and-strong.md) then emplace the metadata of the originating transaction into the slot specified or into a new slot if no slot is specified

### Definition

{% tabs %}
{% tab title="First Tab" %}
```c
int64_t meta_slot (
  	uint32_t slot_no
);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function meta_slot(slotno: number): ErrorCode | number
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t meta_slot_no = 
		meta_slot(0);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
meta_slot(slotno)
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
| Name   | Type   | Description                               |
| ------ | ------ | ----------------------------------------- |
| slotno | number | The slot number to retrieve metadata for. |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The slot the otxn was placed in<br><br><code>INVALID_ARGUMENT</code><br>- specified slot number exceeds the largest possible slot number<br><br><code>NO_FREE_SLOTS</code><br>- the request could not granted because no free slot was avaialble to place the originating transaction into.<br><br><code>PREREQUISITE_NOT_MET</code><br>- The hook is being <a href="../../../concepts/weak-and-strong.md">Strongly Executed</a> and therefore no transactional metadata is available.</p> |
{% endtab %}

{% tab title="Javascript" %}
| Type                | Description                                   |
| ------------------- | --------------------------------------------- |
| ErrorCode \| number | Returns an error code or the slot's metadata. |
{% endtab %}
{% endtabs %}

