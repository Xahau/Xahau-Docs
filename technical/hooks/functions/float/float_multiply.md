---
description: Multiply two XFL numbers together
---

# float\_multiply

### Concepts

* [Floating Point Numbers (XFL)](../../concepts-and-docs/floating-point-numbers-xfl.md)

### Behaviour

* Compute the multiplication of two XFL (xls17) floating point numbers
* Return a new XFL as an int64\_t

### Definition

C

```c
int64_t float_multiply (
    int64_t float1,
    int64_t float2
);
```

### Example

C

```c
int64_t max_vault_pusd =
    float_multiply(vault_xrp, exchange_rate);
```

### Parameters

| Name   | Type     | Description                                                                                  |
| ------ | -------- | -------------------------------------------------------------------------------------------- |
| float1 | int64\_t | An XFL floating point enclosing number representing the first operand to the multiplication  |
| float2 | int64\_t | An XFL floating point enclosing number representing the second operand to the multiplication |

> ### 🚧Caution
>
> Certain multiplications may overflow, which return with an `INVALID_FLOAT` error. However an **underflow** returns as XFL Canonical Zero (i.e. enclosing number = 0).

### Return Code

| Type     | Description                                                                                                                                                                                                                                                                       |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The XFL (xls17) enclosing number<br><br>If negative, an error:<br><code>INVALID_FLOAT</code><br>- one of the supplied parameters was not a valid XFL enclosing number<br><br><code>OVERFLOW</code><br>- the result of the multiplication was too large to store in an XFL.</p> |
