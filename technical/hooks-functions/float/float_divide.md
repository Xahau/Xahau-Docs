---
description: Divide an XFL by another XFL floating point number
---

# float\_divide

### Concepts

* [Floating Point Numbers (XFL)](../../../concepts/floating-point-numbers-xfl.md)

### Behaviour

{% tabs %}
{% tab title="C" %}
* Divide an XFL by another XFL
* Return a new XFL as an int64\_t
{% endtab %}

{% tab title="Javascript" %}
* Divides one float representation by another.
* An error code or the quotient as a bigint.
{% endtab %}
{% endtabs %}



### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t float_divide (
    int64_t float1,
    int64_t float2
);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
 function float_divide(f1: bigint, f2: bigint): ErrorCode | bigint
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t still_one =
    float_divide(float_one(), float_one());
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
float_divide(f1, f2)
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}
| Name   | Type     | Description                                                  |
| ------ | -------- | ------------------------------------------------------------ |
| float1 | int64\_t | An XFL floating point enclosing number to act as numerator   |
| float2 | int64\_t | An XFL floating point enclosing number to act as denominator |
{% endtab %}

{% tab title="Javascript" %}
| Name | Type   | Description         |
| ---- | ------ | ------------------- |
| f1   | bigint | The dividend float. |
| f2   | bigint | The divisor float.  |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="First Tab" %}
| Type     | Description                                                                                                                                                                                                                                                                                                    |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The XFL (xls17) enclosing number<br><br>If negative, an error:<br><code>INVALID_FLOAT</code><br>- the supplied parameter was not a valid XFL enclosing number or the division resulted in an XFL that cannot be represented.<br><br><code>DIVISION_BY_ZERO</code><br>- the supplied parameter was zero.</p> |
{% endtab %}

{% tab title="Second Tab" %}
| Type                | Description                                |
| ------------------- | ------------------------------------------ |
| bigint or ErrorCode | An error code or the quotient as a bigint. |
{% endtab %}
{% endtabs %}

