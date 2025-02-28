---
description: Get the generation of the originating transaction
---

# otxn\_generation

### Behaviour

{% tabs %}
{% tab title="C" %}
* Return the generation of the originating transaction or `1` if no generation field is present.
{% endtab %}

{% tab title="Javascript" %}
* Retrieve the generation number of the originating transaction.
* Returns the generation number as a number.
{% endtab %}
{% endtabs %}

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t otxn_generation (
    void
);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function otxn_generation(): number
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t generation = 
  otxn_generation();
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
const generation = otxn_generation()
```
{% endtab %}
{% endtabs %}



### Parameters

None

### Return Code

{% tabs %}
{% tab title="C" %}
| Type   | Description                                |
| ------ | ------------------------------------------ |
| number | Returns the generation number as a number. |
{% endtab %}

{% tab title="Javascript" %}
| Type     | Description                                                                                                        |
| -------- | ------------------------------------------------------------------------------------------------------------------ |
| int64\_t | The generation of the originating transaction, or `1` if no generation was present on the originating transaction. |
{% endtab %}
{% endtabs %}

