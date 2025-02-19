---
description: Perform a comparison on two XFL floating point numbers
---

# float\_compare

### Concepts

* [Floating Point Numbers (XFL)](../../../concepts/floating-point-numbers-xfl.md)

### Behaviour

* Evaluate a comparison of two XFL floating point numbers
* Return the result of the comparison as a boolean encoded in an int64\_t.

### Definition

C

```c
int64_t float_compare (
    int64_t float1,
    int64_t float2,
    uint32_t mode
);
```

### Example

C

```c
if (float_compare(pusd_to_send, 0, COMPARE_LESS) == 1)
{
  // pusd_to_send is less than 0
}
```

### Parameters

| Name   | Type      | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ------ | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| float1 | int64\_t  | An XFL floating point enclosing number representing the first operand to the comparison                                                                                                                                                                                                                                                                                                                                                                                                                |
| float2 | int64\_t  | An XFL floating point enclosing number representing the second operand to the comparison                                                                                                                                                                                                                                                                                                                                                                                                               |
| mode   | uint32\_t | <p>A bit-flag field consisting of any of (or any logically valid combination of) the following flags:<br><code>COMPARE_LESS</code><br><code>COMPARE_EQUAL</code><br><code>COMPARE_GREATER</code><br><br>Valid combinations are:<br><code>COMPARE_LESS</code> | <code>COMPARE_GREATER</code><br>- Not equal<br><br><code>COMPARE_LESS</code> | <code>COMPARE_EQUAL</code><br>- Less than or equal to<br><br><code>COMPARE_GREATER</code> | <code>COMPARE_EQUAL</code><br>- Greater than or equal to</p> |

> ### 🚧Caution
>
> Always verify the function returned `1` rather than `non-zero`, as negative error codes will be classed as `non-zero`.

### Return Code

| Type     | Description                                                                                                                                                                                                                                                                                                                                           |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p><code>0</code> if the comparison was logically false.<br><code>1</code> if the comparison was logically true.<br><br>If negative, an error:<br><code>INVALID_FLOAT</code><br>- one of the supplied parameters was not a valid XFL enclosing number<br><br><code>INVALID_ARGUMENT</code><br>- invalid combination of supplied comparison flags.</p> |
