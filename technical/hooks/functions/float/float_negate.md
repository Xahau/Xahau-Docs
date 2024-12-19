---
description: Negate an XFL floating point number
---

# float\_negate

### Concepts

* [Floating Point Numbers (XFL)](../../concepts-and-docs/floating-point-numbers-xfl.md)

### Behaviour

* Multiply an XFL by `-1`
* Return a new XFL as an int64\_t

### Definition

C

```c
int64_t float_negate (
    int64_t float1
);
```

### Example

C

```c
int64_t negative_one =
    float_negate(float_one());
```

> ### 📘Special case
>
> The negation of Canonical Zero is Canonical Zero. Unlike some floating point standards (such as IEEE) there is no "negative zero" in XFL.

### Parameters

| Name   | Type     | Description                            |
| ------ | -------- | -------------------------------------- |
| float1 | int64\_t | An XFL floating point enclosing number |

### Return Code

| Type     | Description                                                                                                                                                                  |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The XFL (xls17) enclosing number<br><br>If negative, an error:<br><code>INVALID_FLOAT</code><br>- one of the supplied parameters was not a valid XFL enclosing number</p> |
