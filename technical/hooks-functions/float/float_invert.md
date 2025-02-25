---
description: Divide one by an XFL floating point number
---

# float\_invert

### Concepts

* [Floating Point Numbers (XFL)](../../../concepts/floating-point-numbers-xfl.md)

### Behaviour

{% tabs %}
{% tab title="C" %}
* Inverts a float representation.
* Return a inverted float as a bigint or an ErrorCode
{% endtab %}

{% tab title="Javascript" %}
* Divide `1` by an XFL
* Return a new XFL as an int64\_t
{% endtab %}
{% endtabs %}



### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t float_invert (
    int64_t float1
);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
function float_invert(f1: bigint): ErrorCode | bigint
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t still_one =
    float_invert(float_one());
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
float_invert(f1)
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
| Name | Type  | Description         |
| ---- | ----- | ------------------- |
| f1   | float | The float to invert |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                                                                                                                                                                                    |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The XFL (xls17) enclosing number<br><br>If negative, an error:<br><code>INVALID_FLOAT</code><br>- the supplied parameter was not a valid XFL enclosing number or the division resulted in an XFL that cannot be represented.<br><br><code>DIVISION_BY_ZERO</code><br>- the supplied parameter was zero.</p> |
{% endtab %}

{% tab title="Javascript" %}
| Type                | Description                                      |
| ------------------- | ------------------------------------------------ |
| ErrorCode \| bigint | An error code or the inverted float as a bigint. |
{% endtab %}
{% endtabs %}

