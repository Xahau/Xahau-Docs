---
description: Returns the position in the hook chain the currently executing hook occupies
---

# hook\_pos

### Behaviour

* Returns the position in the hook chain the currently executing hook occupies

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t hook_pos (void);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
hook_pos()
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t pos = 
  	hook_pos();
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
hook_pos()
```
{% endtab %}
{% endtabs %}



### Parameters

This API has no parameters

### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                               |
| -------- | ----------------------------------------------------------------------------------------- |
| int64\_t | The position in the chain the currently executing hook occupies. The first position is 0. |
{% endtab %}

{% tab title="Javascript" %}
| Type   | Description                                                                              |
| ------ | ---------------------------------------------------------------------------------------- |
| number | Returns the current position in the hook chain, or an error code if the retrieval fails. |
{% endtab %}
{% endtabs %}

