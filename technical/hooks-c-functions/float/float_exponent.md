---
description: Get the exponent of an XFL enclosing number
---

# float\_exponent

> ### 🚧 Replaced by macro
>
> This function was replaced by a macro. Please use the macro below in your code instead.\
> To check the validity of the XFL please use float\_mantissa in conjunction with this macro.

### Concepts

* [Floating Point Numbers (XFL)](../../../concepts/floating-point-numbers-xfl.md)

### Behaviour

* Return the exponent part of an XFL as a signed integer

### Definition

Because exponents can be negative, and because negatives are reserved for error states, exponents cannot be returned from functions. Therefore this function has become a macro as shown below.

C

```c
#define float_exponent(f)\
        (((int32_t)(((f) >> 54U) & 0xFFU)) - 97)
```

### Example

C

```c
int64_t exponent =
    float_exponent(float_one());
```

### Parameters

| Name   | Type     | Description                            |
| ------ | -------- | -------------------------------------- |
| float1 | int64\_t | An XFL floating point enclosing number |
