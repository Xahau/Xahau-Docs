---
description: Serialize and output the xpop transaction blob and metadata
---

# xpop\_slot

### Behaviour

* Locate the xpop blob on the `Import` transaction
* Emplace the located tx and meta objects into the slots specified

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t xpop_slot (
  	uint32_t slot_no_tx,
  	uint32_t slot_no_meta
);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
function xpop_slot(slotno_tx: number, slotno_meta: number): ErrorCode | number
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t bytes_written = 
    xpop_slot(1, 2); // assumes a txn is slotted into slot=1 meta is slotted into slot=2
```
{% endtab %}

{% tab title="Javacript" %}
```javascript
xpop_slot(slotno_tx, slotno_meta)
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}
| Name           | Type      | Description                                    |
| -------------- | --------- | ---------------------------------------------- |
| slot\_no\_tx   | uint32\_t | The slot number to emplace the tx blob into.   |
| slot\_no\_meta | uin32\_t  | The slot number to emplace the meta blob into. |
{% endtab %}

{% tab title="Javascript" %}
| Name         | Type   | Description                         |
| ------------ | ------ | ----------------------------------- |
| slotno\_tx   | number | The transaction slot number to pop. |
| slotno\_meta | number | The metadata slot number to pop.    |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                                                                                                                                |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p><code>PREREQUISITE_NOT_MET</code><br><br>- The originating tx type was not <code>Import</code>.<br><br><code>NO_FREE_SLOTS</code><br><br>- The API would require a new slot to be allocated but the Hook is already at the maximum number of slots.</p> |
{% endtab %}

{% tab title="Javascript" %}
| Type                | Description                                               |
| ------------------- | --------------------------------------------------------- |
| number or ErrorCode | Returns an error code or the result of the pop operation. |
{% endtab %}
{% endtabs %}

