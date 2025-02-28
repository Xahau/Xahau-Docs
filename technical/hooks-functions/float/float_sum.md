---
description: Add two XFL numbers together
---

# float\_sum

### Concepts

* [Floating Point Numbers (XFL)](../../../concepts/floating-point-numbers-xfl.md)

### Behaviour

{% tabs %}
{% tab title="C" %}
* Compute the addition of two XFL (xls17) floating point numbers
* Return a new XFL as an int64\_t
{% endtab %}

{% tab title="Javascript" %}
* Sums two float representations.
* Returns an error code or the sum as a bigint.
{% endtab %}
{% endtabs %}

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t float_sum (
    int64_t float1,
    int64_t float2
);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
function float_sum(f1: bigint, f2: bigint): ErrorCode | bigint
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t two =
    float_sum(float_one(), float_one());
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
const two =
  float_sum(float_one(), float_one());
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}


| Name   | Type     | Description                                                                            |
| ------ | -------- | -------------------------------------------------------------------------------------- |
| float1 | int64\_t | An XFL floating point enclosing number representing the first operand to the addition  |
| float2 | int64\_t | An XFL floating point enclosing number representing the second operand to the addition |

> ### 📘Hint
>
> To subtract two floats use `float_negate` on the second float then use `float_sum`.
{% endtab %}

{% tab title="Javascript" %}


| Name | Type   | Description              |
| ---- | ------ | ------------------------ |
| f1   | bigint | The first float to sum.  |
| f2   | bigint | The second float to sum. |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                                                                                                                                                 |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The XFL (xls17) enclosing number<br><br>If negative, an error:<br><code>INVALID_FLOAT</code><br>- one of the supplied parameters was not a valid XFL enclosing number<br><br><code>OVERFLOW</code><br>- the result of the addition was too large to store in an XFL.</p> |
{% endtab %}

{% tab title="Javascript" %}
| Type                | Description                           |
| ------------------- | ------------------------------------- |
| ErrorCode or bigint | An error code or the sum as a bigint. |
{% endtab %}
{% endtabs %}

