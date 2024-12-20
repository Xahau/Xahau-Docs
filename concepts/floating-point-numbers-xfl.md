---
description: High precision calculations are native to Hooks.
---

# Floating Point Numbers (XFL)

### Background

[Floating point numbers](https://en.wikipedia.org/wiki/Floating-point_arithmetic) are widely used in computer science to do calculation of finite precision but arbitrary scale numbers.

Most modern CPUs are capable of performing fast floating point operations using the [IEEE binary floating point standard](https://en.wikipedia.org/wiki/Double-precision_floating-point_format) however `xahaud` does **not** use this format. Instead Xahau uses a [bespoke decimal floating point standard](https://xrpl.org/serialization.html#issued-currency-amount-format).

This custom format has three basic properties:

1. The format is inherently decimal, expressed as a decimal `mantissa` multipled by `10` to the power of an `exponent`.
2. All values expressed have 16 significant (decimal) figures.
3. The range of exponents is `-96` to `+80`

When serialized the mantissa is 54 bits, and the exponent is 8 bits, with a final sign bit bringing the total size of the serialized floating point to 63 bits.

### What is XFL?

[XLS-17d](https://github.com/XRPLF/XRPL-Standards/discussions/39) is an XRPL standards proposal that defines an efficient way to pack and store xrpld floating point numbers (as described above).

XFLs store the bits of the floating point number within an _enclosing number_. This is always an `int64_t`. Negative enclosing numbers represent invalid XFLs (for example as a result of division by zero.)

> 📘 Hint
>
> Use the XFL-tool [here](https://richardah.github.io/xfl-tools/) to compose and decompose XFLs in your browser!

Some example XFLs follow

| loating Point Value | Enclosing Number    | Representation                |
| ------------------- | ------------------- | ----------------------------- |
| -1                  | 1478180677777522688 | -1000000000000000 \* 10^(-15) |
| 0                   | 0                   | 0 (_canonical zero_)          |
| 1                   | 6089866696204910592 | +1000000000000000 \* 10^(-15) |
| _PI_                | 6092008288858500385 | +3141592653589793 \* 10^(-15) |
| -_PI_               | 1480322270431112481 | -3141592653589793 \* 10^(-15) |

This format is very convenient for Hooks, as Hooks can only exchange _integer_ values with xrpld. By enclosing the floating point inside an integer in a well defined way it becomes possible to do complex floating point computations from a Hook. This is useful for computing exchange rates.

### Canonical Zero

Floating point regimes typically have a number of different ways to express zero, which can be a problem for testing for zero. For example `0 x 10 ^ 1` is zero and `0 x 10 ^ 2` is also zero. For this reason there is a canonical zero enforced by the standard and the Hook API. The canonical zero is also enclosing number zero (`0`).

### Hook Float API

Once you have an XFL you can use the Float API to do various computations. The Float API appears in the table below. Each API takes one or more XFL enclosing numbers and returns an XFL enclosing number. Negative return values _always_ represent a computational error (such as division by zero). There are no valid negative enclosing numbers.

| Hook API                                                                  | What it does                                                          |
| ------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| [float\_set](../technical/hooks-c-functions/float/float_set.md)           | Create a float from an exponent and mantissa                          |
| [float\_multiply](../technical/hooks-c-functions/float/float_multiply.md) | Multiply two XFL numbers together                                     |
| [float\_mulratio](../technical/hooks-c-functions/float/float_mulratio.md) | Multiply an XFL floating point by a non-XFL numerator and denominator |
| [float\_negate](../technical/hooks-c-functions/float/float_negate.md)     | Negate an XFL floating point number                                   |
| [float\_compare](../technical/hooks-c-functions/float/float_compare.md)   | Perform a comparison on two XFL floating point numbers                |
| [float\_sum](../technical/hooks-c-functions/float/float_sum.md)           | Add two XFL numbers together                                          |
| [float\_sto](../technical/hooks-c-functions/float/float_sto.md)           | Output an XFL as a serialized object                                  |
| [float\_sto\_set](../technical/hooks-c-functions/float/float_sto_set.md)  | Read a serialized amount into an XFL                                  |
| [float\_invert](../technical/hooks-c-functions/float/float_invert.md)     | Divide one by an XFL floating point number                            |
| [float\_divide](../technical/hooks-c-functions/float/float_divide.md)     | Divide an XFL by another XFL floating point number                    |
| [float\_one](../technical/hooks-c-functions/float/float_one.md)           | Return the number 1 represented in an XFL enclosing number            |
| [float\_exponent](../technical/hooks-c-functions/float/float_exponent.md) | Get the exponent of an XFL enclosing number                           |
| [float\_mantissa](../technical/hooks-c-functions/float/float_mantissa.md) | Get the mantissa of an XFL enclosing number                           |
| [float\_sign](../technical/hooks-c-functions/float/float_sign.md)         | Get the sign of an XFL enclosing number                               |
| float\_exponent\_set                                                      | Set the exponent of an XFL enclosing number                           |
| float\_mantissa\_set                                                      | Set the mantissa of an XFL enclosing number                           |
| float\_sign\_set                                                          | Set the sign of an XFL enclosing number                               |
| [float\_int](../technical/hooks-c-functions/float/float_int.md)           | Convert an XFL floating point into an integer (floor)                 |
| [float\_root](../technical/hooks-c-functions/float/float_root.md)         | Compute the nth root of an XFL                                        |
| [float\_log](../technical/hooks-c-functions/float/float_log.md)           | Compute the decimal log of an XFL                                     |

> ❗️ Warning
>
> You should never do any direct math or comparison on the _enclosing number_. This will almost always result in incorrect computations.
>
> The _sole exception_ is checking for canonical zero.

### Example

In the below example an exchange rate conversion is performed, followed by a high precision fraction multiplication.

```c
int64_t max_vault_pusd =
    float_multiply(vault_xrp, exchange_rate);

max_vault_pusd = 
    float_mulratio(max_vault_pusd, 0,
        NEW_COLLATERALIZATION_NUMERATOR, NEW_COLLATERALIZATION_DENOMINATOR);
```

> 🚧 Tip
>
> If a float API returns a negative value and you do no check for negatives then feeding that negative value into another float API will also produce a negative value. In this way errors are propagated much as `NaN` (not a number) is propagated in other languages.
>
> If you ever end up with a negative enclosing number an error occured somewhere in your floating point calculations.
