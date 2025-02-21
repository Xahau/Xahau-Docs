---
description: Multiply two XFL numbers together
---

# float\_multiply

### Concepts

* [Floating Point Numbers (XFL)](../../../concepts/floating-point-numbers-xfl.md)

### Behaviour

{% tabs %}
{% tab title="C" %}
* Compute the multiplication of two XFL (xls17) floating point numbers
* Return a new XFL as an int64\_t
{% endtab %}

{% tab title="Javascript" %}
* Compute the multiplication of two XFL (xls17) floating point numbers
* Return n error code or the product as a bigint.
{% endtab %}
{% endtabs %}



### Definition

{% tabs %}
{% tab title="C" %}
<pre class="language-c"><code class="lang-c"><strong>int64_t float_multiply (
</strong><strong>    int64_t float1,
</strong><strong>    int64_t float2
</strong>);
</code></pre>


{% endtab %}

{% tab title="Javascript" %}
```javascript
function float_multiply(f1: bigint, f2: bigint): ErrorCode | bigint
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t max_vault_pusd =
    float_multiply(vault_xrp, exchange_rate);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
float_multiply(f1, f2)
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}


| Name   | Type     | Description                                                                                  |
| ------ | -------- | -------------------------------------------------------------------------------------------- |
| float1 | int64\_t | An XFL floating point enclosing number representing the first operand to the multiplication  |
| float2 | int64\_t | An XFL floating point enclosing number representing the second operand to the multiplication |

> ### 🚧Caution
>
> Certain multiplications may overflow, which return with an `INVALID_FLOAT` error. However an **underflow** returns as XFL Canonical Zero (i.e. enclosing number = 0).
{% endtab %}

{% tab title="Javascript" %}
| Name | Type   | Description                                                                                  |
| ---- | ------ | -------------------------------------------------------------------------------------------- |
| f1   | bigint | An XFL floating point enclosing number representing the first operand to the multiplication  |
| f2   | bigint | An XFL floating point enclosing number representing the second operand to the multiplication |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}


| Type     | Description                                                                                                                                                                                                                                                                       |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The XFL (xls17) enclosing number<br><br>If negative, an error:<br><code>INVALID_FLOAT</code><br>- one of the supplied parameters was not a valid XFL enclosing number<br><br><code>OVERFLOW</code><br>- the result of the multiplication was too large to store in an XFL.</p> |
{% endtab %}

{% tab title="Javascript" %}


| Type               | Description                               |
| ------------------ | ----------------------------------------- |
| Errorcor or bigint | An error code or the product as a bigint. |
{% endtab %}
{% endtabs %}

