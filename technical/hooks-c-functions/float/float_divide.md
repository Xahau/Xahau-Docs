---
description: Divide an XFL by another XFL floating point number
---

# float\_divide

### Concepts

* [Floating Point Numbers (XFL)](../../../concepts/floating-point-numbers-xfl.md)

### Behaviour

* Divide an XFL by another XFL
* Return a new XFL as an int64\_t

### Definition

C

```c
int64_t float_divide (
    int64_t float1,
    int64_t float2
);
```

### Example

C

```c
int64_t still_one =
    float_divide(float_one(), float_one());
```

### Parameters

| Name   | Type     | Description                                                  |
| ------ | -------- | ------------------------------------------------------------ |
| float1 | int64\_t | An XFL floating point enclosing number to act as numerator   |
| float2 | int64\_t | An XFL floating point enclosing number to act as denominator |

### Return Code

| Type     | Description                                                                                                                                                                                                                                                                                                    |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The XFL (xls17) enclosing number<br><br>If negative, an error:<br><code>INVALID_FLOAT</code><br>- the supplied parameter was not a valid XFL enclosing number or the division resulted in an XFL that cannot be represented.<br><br><code>DIVISION_BY_ZERO</code><br>- the supplied parameter was zero.</p> |
