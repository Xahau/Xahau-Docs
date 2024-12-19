---
description: Get the mantissa of an XFL enclosing number
---

# float\_mantissa

### Concepts

* [Floating Point Numbers (XFL)](../../concepts-and-docs/floating-point-numbers-xfl.md)

### Behaviour

* Return the mantissa part of an XFL as an unsigned integer

### Definition

C

```c
int64_t float_mantissa (
    int64_t float1
);
```

### Example

C

```c
int64_t exponent =
    float_exponent(float_one());
```

> ### 📘Hint
>
> The mantissa of a negative XFL is positive. Use `float_sign` to get the sign.

### Parameters

| Name   | Type     | Description                            |
| ------ | -------- | -------------------------------------- |
| float1 | int64\_t | An XFL floating point enclosing number |

### Return Code

| Type     | Description                                                                                                                                                 |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The mantissa of the XFL<br><br>If negative, an error:<br><code>INVALID_FLOAT</code><br>- the supplied parameter was not a valid XFL enclosing number</p> |
