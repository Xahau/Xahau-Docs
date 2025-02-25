---
description: Get the mantissa of an XFL enclosing number
---

# float\_mantissa

### Concepts

* [Floating Point Numbers (XFL)](../../../concepts/floating-point-numbers-xfl.md)

### Behaviour

{% tabs %}
{% tab title="C" %}
* Return the mantissa part of an XFL as an unsigned integer
{% endtab %}

{% tab title="Javascript" %}
* Retrieves the mantissa of a float representation.
* An error code or the mantissa as a bigint.
{% endtab %}
{% endtabs %}



### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t float_mantissa (
    int64_t float1
);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function float_mantissa(f1: bigint): ErrorCode | bigint
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t exponent =
    float_exponent(float_one());
```

> ### 📘Hint
>
> The mantissa of a negative XFL is positive. Use `float_sign` to get the sign.
{% endtab %}

{% tab title="Javascript" %}
```javascript
float_mantissa(f1)
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}
| Name | Type   | Description                              |
| ---- | ------ | ---------------------------------------- |
| f1   | bigint | The float to retrieve the mantissa from. |
{% endtab %}

{% tab title="Javascript" %}
| Name   | Type     | Description                            |
| ------ | -------- | -------------------------------------- |
| float1 | int64\_t | An XFL floating point enclosing number |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                                 |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The mantissa of the XFL<br><br>If negative, an error:<br><code>INVALID_FLOAT</code><br>- the supplied parameter was not a valid XFL enclosing number</p> |
{% endtab %}

{% tab title="Javascript" %}
| Type                | Description                                |
| ------------------- | ------------------------------------------ |
| bigint or ErrorCode | An error code or the mantissa as a bigint. |
{% endtab %}
{% endtabs %}

