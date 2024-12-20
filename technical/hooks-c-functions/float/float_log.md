---
description: Compute the decimal log of an XFL
---

# float\_log

### Concepts

* [Floating Point Numbers (XFL)](../../../concepts/floating-point-numbers-xfl.md)

### Behaviour

* Compute a the decimal logarithm of an XFL number
* Return the new XFL

> ### ❗️Warning
>
> Due to speed constraints,`float_log` converts the argument to an IEEE base-2 double precision floating point before applying base 10 log. Therefore the returned result will often contain less precision than expected.

### Definition

C

```c
int64_t float_log (
    int64_t float1
);
```

### Example

C

```c
int64_t zero =
    float_log(float_one());
```

> ### 🚧Warning
>
> If a negative number is passed the function will return `COMPLEX_NOT_SUPPORTED` if the root is an even root.

### Parameters

| Name   | Type     | Description                                                                                            |
| ------ | -------- | ------------------------------------------------------------------------------------------------------ |
| float1 | int64\_t | An XFL floating point enclosing number representing the floating point number to take the logarithm of |

### Return Code

| Type     | Description                                                                                                                                                                                                                                                                                          |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The computed logarithm<br><br>If negative, an error:<br><code>INVALID_FLOAT</code><br>- the supplied parameter was not a valid XFL enclosing number<br><br><code>COMPLEX_NOT_SUPPORTED</code><br>- the supplied parameter was a negative number which would result in a complex return value.</p> |
