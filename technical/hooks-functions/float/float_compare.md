---
description: Perform a comparison on two XFL floating point numbers
---

# float\_compare

### Concepts

* [Floating Point Numbers (XFL)](../../../concepts/floating-point-numbers-xfl.md)

### Behaviour

{% tabs %}
{% tab title="C" %}
* Evaluate a comparison of two XFL floating point numbers
* Return the result of the comparison as a boolean encoded in an int64\_t.
{% endtab %}

{% tab title="Javascript" %}
* Evaluate a comparison of two XFL floating point numbers
* Returns an error code or the comparison result as a number.
{% endtab %}
{% endtabs %}



### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t float_compare (
    int64_t float1,
    int64_t float2,
    uint32_t mode
);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function float_compare(
    f1: bigint,
    f2: bigint,
    mode: number
  ): ErrorCode | number
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
if (float_compare(pusd_to_send, 0, COMPARE_LESS) == 1)
{
  // pusd_to_send is less than 0
}
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
float_compare(f1, f2, mode)
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}


| Name   | Type      | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ------ | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| float1 | int64\_t  | An XFL floating point enclosing number representing the first operand to the comparison                                                                                                                                                                                                                                                                                                                                                                                                                |
| float2 | int64\_t  | An XFL floating point enclosing number representing the second operand to the comparison                                                                                                                                                                                                                                                                                                                                                                                                               |
| mode   | uint32\_t | <p>A bit-flag field consisting of any of (or any logically valid combination of) the following flags:<br><code>COMPARE_LESS</code><br><code>COMPARE_EQUAL</code><br><code>COMPARE_GREATER</code><br><br>Valid combinations are:<br><code>COMPARE_LESS</code> | <code>COMPARE_GREATER</code><br>- Not equal<br><br><code>COMPARE_LESS</code> | <code>COMPARE_EQUAL</code><br>- Less than or equal to<br><br><code>COMPARE_GREATER</code> | <code>COMPARE_EQUAL</code><br>- Greater than or equal to</p> |

> ### 🚧Caution
>
> Always verify the function returned `1` rather than `non-zero`, as negative error codes will be classed as `non-zero`.
{% endtab %}

{% tab title="Javascript" %}


| Name | Type   | Description                                                    |
| ---- | ------ | -------------------------------------------------------------- |
| f1   | bigint | The first float to compare.                                    |
| f2   | bigint | The second float to compare.                                   |
| mode | number | The comparison mode (e.g., less than, equal to, greater than). |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}


| Type     | Description                                                                                                                                                                                                                                                                                                                                           |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p><code>0</code> if the comparison was logically false.<br><code>1</code> if the comparison was logically true.<br><br>If negative, an error:<br><code>INVALID_FLOAT</code><br>- one of the supplied parameters was not a valid XFL enclosing number<br><br><code>INVALID_ARGUMENT</code><br>- invalid combination of supplied comparison flags.</p> |
{% endtab %}

{% tab title="Javascript" %}


| Type                | Description                                                 |
| ------------------- | ----------------------------------------------------------- |
| ErrorCode or number | Returns an error code or the comparison result as a number. |
{% endtab %}
{% endtabs %}

