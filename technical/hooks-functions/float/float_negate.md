---
description: Negate an XFL floating point number
---

# float\_negate

### Concepts

* [Floating Point Numbers (XFL)](../../../concepts/floating-point-numbers-xfl.md)

### Behaviour

{% tabs %}
{% tab title="C" %}
* Multiply an XFL by `-1`
* Return a new XFL as an int64\_t
{% endtab %}

{% tab title="Javascript" %}
* Negates a float representation.
* Returns an error code or the negated float as a bigint.
{% endtab %}
{% endtabs %}

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t float_negate (
    int64_t float1
);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
function float_negate(f1: bigint): ErrorCode | bigint
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t negative_one =
    float_negate(float_one());
```

> ### 📘Special case
>
> The negation of Canonical Zero is Canonical Zero. Unlike some floating point standards (such as IEEE) there is no "negative zero" in XFL.


{% endtab %}

{% tab title="Javascript" %}
```javascript
const negative_one =
    float_negate(float_one());
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


| Name | Type   | Description          |
| ---- | ------ | -------------------- |
| f1   | bigint | The float to negate. |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                                                  |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The XFL (xls17) enclosing number<br><br>If negative, an error:<br><code>INVALID_FLOAT</code><br>- one of the supplied parameters was not a valid XFL enclosing number</p> |


{% endtab %}

{% tab title="Javascript" %}
| Type                | Description                                        |
| ------------------- | -------------------------------------------------- |
| ErrorCode or bigint | An error code or The XFL (xls17) enclosing number. |
{% endtab %}
{% endtabs %}

