---
description: Return the number 1 represented in an XFL enclosing number
---

# float\_one

### Concepts

* [Floating Point Numbers (XFL)](../../../concepts/floating-point-numbers-xfl.md)

### Behaviour

* Return one(`1`) as an XFL int64\_t

### Definition

C

```c
int64_t float_one ();
```

### Example

C

```c
int64_t still_one =
    float_one();
```

### Parameters

This function has no parameters.

### Return Code

| Type     | Description                      |
| -------- | -------------------------------- |
| int64\_t | The XFL (xls17) enclosing number |
