---
description: Get the sign of an XFL enclosing number
---

# float\_sign

### Concepts

* [Floating Point Numbers (XFL)](../../../concepts/floating-point-numbers-xfl.md)

### Behaviour

{% tabs %}
{% tab title="C" %}
* Return `1` if the XFL is negative, otherwise return 0
{% endtab %}

{% tab title="Javascript" %}
* Return 1 if the XFL is negative, otherwise return 0
{% endtab %}
{% endtabs %}

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t float_sign (
    int64_t float1
);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function float_sign(f1: bigint): ErrorCode | number
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t sign =
    float_sign(float_one());
```

> ### 📘Hint
>
> The sign bit inside the XFL is the `0` when the XFL is negative, however this function follows the standard computing convention to return `1` if it is negative.
{% endtab %}

{% tab title="Javascript" %}
```javascript
const sign =
   float_sign(float_one());
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}
| Name   | Type     | Description                            |
| ------ | -------- | -------------------------------------- |
| float1 | int64\_t | An XFL floating point enclosing number |
{% endtab %}

{% tab title="Javascript" %}
| Name | Type   | Description                              |
| ---- | ------ | ---------------------------------------- |
| f1   | bigint | The float to retrieve the mantissa from. |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                                                                                         |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The sign of the XFL:<br><code>0</code> if positive, <code>1</code> if negative.<br><br>If negative, an error:<br><code>INVALID_FLOAT</code><br>- the supplied parameter was not a valid XFL enclosing number</p> |


{% endtab %}

{% tab title="Javascript" %}
| Type                | Description                                |
| ------------------- | ------------------------------------------ |
| bigint or ErrorCode | An error code or the mantissa as a bigint. |
{% endtab %}
{% endtabs %}

