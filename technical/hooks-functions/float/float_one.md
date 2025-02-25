---
description: Return the number 1 represented in an XFL enclosing number
---

# float\_one

### Concepts

* [Floating Point Numbers (XFL)](../../../concepts/floating-point-numbers-xfl.md)

### Behaviour

{% tabs %}
{% tab title="C" %}
* Return one(`1`) as an XFL int64\_t
{% endtab %}

{% tab title="Javascript" %}
* Retrieves the float representation of a number.
{% endtab %}
{% endtabs %}



### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t float_one ();
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function float_one(): ErrorCode | bigint
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t still_one =
    float_one();
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
float_one()
```
{% endtab %}
{% endtabs %}



### Parameters

This function has no parameters.

### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                      |
| -------- | -------------------------------- |
| int64\_t | The XFL (xls17) enclosing number |
{% endtab %}

{% tab title="Javascript" %}
| Type     | Description                      |
| -------- | -------------------------------- |
| int64\_t | The XFL (xls17) enclosing number |
{% endtab %}
{% endtabs %}

