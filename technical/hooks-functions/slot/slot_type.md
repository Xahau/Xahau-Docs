---
description: >-
  Retrieve the field code of an object in a slot and, optionally, some other
  information
---

# slot\_type

### &#x20;Behaviour

{% tabs %}
{% tab title="C" %}
* Locate the object pointed to by the specified `slot_no`
* Determine its `sf` field code and return this, or some other information (see below) if `flags` are used
{% endtab %}

{% tab title="Javascript" %}
* Retrieves the type of the specified slot.
* Returns an error code or the type of the slot.
{% endtab %}
{% endtabs %}

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t slot_type (
    uint32_t slot_no,
    uint32_t flags
);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function slot_type(slotno: number, flags: number): ErrorCode | number
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
uint8_t txn_id[32];
int64_t bytes_written = 
    slot_id(txn_id, 32, 1); // assumes a txn is slotted into slot=1
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
const txn_id = slot_type(1) // assumes a txn is slotted into slot=1
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}
| Name     | Type      | Description                                                                                                                                                                                                          |
| -------- | --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| slot\_no | uint32\_t | The slot number                                                                                                                                                                                                      |
| flags    | uin32\_t  | <p>For normal operation this should be <code>0</code>.<br><br>To determine whether or not an <code>STI_AMOUNT</code> type contains a native (XAH) amount or a floating point (IOU) amount set to <code>1</code>.</p> |
{% endtab %}

{% tab title="Javascript" %}
| Name   | Type   | Description                           |
| ------ | ------ | ------------------------------------- |
| slotno | number | The slot number to check the type of. |
| flags  | number | Flags to determine the type.          |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>If <code>flags</code> is <code>0</code> then:<br>The <code>sf</code> field code of the slotted object<br><br>If <code>flags</code> is <code>1</code> then:<br><code>1</code> if and only if the slotted object is an <code>STI_AMOUNT</code> and the type of the amount is XAH.<br><br>If negative, an error:<br><code>DOESNT_EXIST</code><br>- the specified <code>slot_no</code> does not contain an object.<br><br><code>NOT_AN_AMOUNT</code><br>- <code>flags</code> was set to <code>1</code> but the slotted object is not an <code>STI_AMOUNT</code> object</p> |
{% endtab %}

{% tab title="Javascript" %}
| Type                | Description                                    |
| ------------------- | ---------------------------------------------- |
| ErrorCode or number | Returns an error code or the type of the slot. |
{% endtab %}
{% endtabs %}

