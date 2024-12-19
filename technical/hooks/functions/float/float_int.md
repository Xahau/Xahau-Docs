---
description: Convert an XFL floating point into an integer (floor)
---

# float\_int

### Concepts

* [Floating Point Numbers (XFL)](../../concepts-and-docs/floating-point-numbers-xfl.md)

### Behaviour

* Left shift (multiply by 10) the XFL by the number of specified decimal places
* Convert the resulting XFL to an integer, discarding any remainder
* Return the integer

### Definition

C

```c
int64_t float_int (
    int64_t float1,
    uint32_t decimal_places,
  	uint32_t absolute
);
```

### Example

C

```c
int64_t drops =
    float_int(xrpbalance, 6, 0);
```

### Parameters

| Name            | Type      | Description                                                                                              |
| --------------- | --------- | -------------------------------------------------------------------------------------------------------- |
| float1          | int64\_t  | An XFL floating point enclosing number representing the first operand to the addition                    |
| decimal\_places | uint32\_t | The number of places to shift the decimal to the right before computing the floor of the floating point. |
| absolute        | uint32\_t | If `1` also take the absolute of the value before returning it.                                          |

> ### 📘Hint
>
> Negative return values are reserved for error codes. Therefore if you need to execute this function against a negative XFL you should use `absolute = 1`

### Return Code

| Type     | Description                                                                                                                                                                                                                                                                                                                                                                                                       |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The computed positive integer<br><br>If negative, an error:<br><code>INVALID_FLOAT</code><br>- one of the supplied parameters was not a valid XFL enclosing number<br><br><code>INVALID_ARGUMENT</code><br>- attempted to specify more than 15 decimal places.<br><br><code>CANT_RETURN_NEGATIVE</code><br>- attempted to return a negative integer but this is not allowed, use <code>absolute = 1</code></p> |
