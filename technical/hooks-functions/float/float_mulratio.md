---
description: Multiply an XFL floating point by a non-XFL numerator and denominator
---

# float\_mulratio

### Concepts

* [Floating Point Numbers (XFL)](../../../concepts/floating-point-numbers-xfl.md)

### Behaviour

* Compute the multiplication of an XFL (xls17) floating point number and the quotient of two integers
* Return a new XFL as an int64\_t

### Definition

C

```c
int64_t float_multiply (
    int64_t float1,
    uint32_t round_up,
    uint32_t numerator,
    uint32_t denominator
);
```

### Example

C

```c
int64_t max_vault_pusd =
    float_mulratio(max_vault_pusd, 0,
        COLLATERALIZATION_NUMERATOR, COLLATERALIZATION_DENOMINATOR);
```

### Parameters

| Name        | Type      | Description                                                                                 |
| ----------- | --------- | ------------------------------------------------------------------------------------------- |
| float1      | int64\_t  | An XFL floating point enclosing number representing the first operand to the multiplication |
| round\_up   | uint32\_t | If non-zero all computations will be rounded up                                             |
| numerator   | uint32\_t | The numerator of the quotient that the float will be multiplied by                          |
| denominator | uint32\_t | The denominator of the quotient that the float will be multiplied by                        |

> ### 🚧Caution
>
> Certain multiplications may overflow, which return with an `INVALID_FLOAT` error. However an **underflow** returns as XFL Canonical Zero (i.e. enclosing number = 0).

### Return Code

| Type     | Description                                                                                                                                                                                                                                                                                                                                                    |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The XFL (xls17) enclosing number<br><br>If negative, an error:<br><code>INVALID_FLOAT</code><br>- one of the supplied parameters was not a valid XFL enclosing number<br><br><code>OVERFLOW</code><br>- the result of the multiplication was too large to store in an XFL.<br><br><code>DIVISION_BY_ZERO</code><br>- the supplied denominator was zero.</p> |
