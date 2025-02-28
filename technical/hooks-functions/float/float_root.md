---
description: Compute the nth root of an XFL
---

# float\_root

### Concepts

* [Floating Point Numbers (XFL)](../../../concepts/floating-point-numbers-xfl.md)

### Behaviour

{% tabs %}
{% tab title="C" %}
* Compute a the `nth` root of an XFL number
* Return the new XFL

> ### ❗️Warning
>
> Due to speed constraints,`float_root` converts the argument to an IEEE base-2 double precision floating point before applying n-th root. Therefore the returned result will often contain less precision than expected. If you need better precision you should consider dividing your XFL into a high and a low product then individually take the square roots of those products and multiply the results together.


{% endtab %}

{% tab title="Javascript" %}
* Calculates the nth root of a float representation.
* An error code or the resulting root as a bigint.
{% endtab %}
{% endtabs %}



### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t float_root (
    int64_t float1,
    uint32_t n
);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
function float_root(f1: bigint, n: number): ErrorCode | bigint
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t three =
    float_root(nine, 2);
```

> ### 🚧Warning
>
> If a negative number is passed the function will return `COMPLEX_NOT_SUPPORTED` if the root is an even root.
{% endtab %}

{% tab title="Javascript" %}
```javascript
const three =
  float_root(nine, 2)
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}
| Name   | Type      | Description                                                                                              |
| ------ | --------- | -------------------------------------------------------------------------------------------------------- |
| float1 | int64\_t  | An XFL floating point enclosing number representing the floating point number to take the square root of |
| n      | uint32\_t | The root to compute, for example `2` is a square root.                                                   |
{% endtab %}

{% tab title="Javascript" %}
| Name | Type   | Description                          |
| ---- | ------ | ------------------------------------ |
| f1   | bigint | The float to calculate the root of.  |
| n    | number | The degree of the root to calculate. |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}


| Type     | Description                                                                                                                                                                                                                                                                                 |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The computed nth root<br><br>If negative, an error:<br><code>INVALID_FLOAT</code><br>- the supplied parameter was not a valid XFL enclosing number<br><br><code>COMPLEX_NOT_SUPPORTED</code><br>- the supplied parameter was a negative number which would result in a complex root.</p> |
{% endtab %}

{% tab title="Javascript" %}


| Type                | Description                                              |
| ------------------- | -------------------------------------------------------- |
| bigint or ErrorCode | Returns an error code or the resulting root as a bigint. |
{% endtab %}
{% endtabs %}

