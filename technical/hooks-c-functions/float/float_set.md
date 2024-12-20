---
description: Create a float from an exponent and mantissa
---

# float\_set

### Concepts

* [Floating Point Numbers (XFL)](../../../concepts/floating-point-numbers-xfl.md)

### Behaviour

* Compute an XFL (xls17) floating point from the provided exponent and mantissa
* Return that XFL as an int64\_t

### Definition

C

```c
int64_t float_set (
    int32_t exponent,
    int64_t mantissa
);
```

### Example

C

```c
int64_t small_amount =
  float_set(-81, 1);
```

### Parameters

| Name     | Type     | Description                                                     |
| -------- | -------- | --------------------------------------------------------------- |
| exponent | int32\_t | An exponent in the range `-96` to `80`                          |
| mantissa | int64\_t | A mantissa. If negative then the sign of the float is negative. |

> ### 🚧Caution
>
> When setting a mantissa that is greater or fewer than 16 decimal digits the exponent will be adjusted to ensure the mantissa is exactly 16 digits. This adjustment may result in an `INVALID_FLOAT` in some circumstances.

> ### 📘Special case
>
> XFL canonical 0 is also 0 in the enclosing number. Thus there is never a need to call `float_set(0,0);`

### Return Code

| Type     | Description                                                                                                                                                                         |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The XFL (xls17) enclosing number<br><br>If negative, an error:<br><code>INVALID_FLOAT</code><br>- The adjustment of the mantissa to 16 digits produced an under or overflow.</p> |
