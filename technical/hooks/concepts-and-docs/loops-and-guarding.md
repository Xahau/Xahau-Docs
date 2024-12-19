---
description: Guards are needed to perform loops in a Hook.
---

# Loops and Guarding

### What are guards?

Hooks are deliberately not [Turing Complete](https://en.wikipedia.org/wiki/Turing_completeness). This means arbitrary looping is forbidden. Instead you must _guard_ your loops against a hard "maximum iteration" boundary.

A guard is a marker placed in your code at the top of each loop. The marker informs the Xahau what the upper bound of your loop will be _in every possible scenario_. Thus if your loop usually executes twice but sometimes executes _500_ times, then your guard will say 500.

Guards are used by the Xahau to determine the _worst case execution time_ (in instructions) of your Hook before execution. This is the basis for the fee the Xahau charges for the execution of a Hook and makes execution times predictable and controllable.

> 🚧  Tip
>
> Existing developers migrating from other smart contract platforms may find guards to be annoying at first but once you get used to them they are no harder to use than a normal for-loop.

### The guard function

The guard function tells the ledger the **maximum number of iterations** a loop will make. Specifically the function takes two arguments:

```c
int32_t _g (uint32_t id, uint32_t maxiter);
```

The first argument `id` is the identifier for this guard. This is a unique constant chosen by the developer, typically the line number in the source file is used.

The second argument `maxiter` is a promise the developer makes to the ledger that this guard will not be _hit_ more than `maxiter` times during the execution of the Hook. If the guard call is executed more than this many times the Hook will automatically rollback with a `GUARD_VIOLATION` ([Hook API return codes](ref:negative-return-codes)). Because the guard will be hit _before_ the loop condition is checked, it is important to add one to the total number of expected iterations. (Note: The GUARD() macro already adds one).

> ❗️ Pay Attention
>
> Guards must be set using numerical literals. You cannot use a variable or runtime value in a Guard.

### Guard enforcement

Consider the following for-loop in C:

```c
#define GUARD(maxiter) _g(__LINE__, (maxiter)+1)
for (int i = 0; GUARD(3), i < 3; ++i)
{
  ...
}
```

In C, the comma operator executes each expression in a list of expressions (e.g. `A, B, C`) and returns the last expression (e.g. `C`). Thus the condition above is still `i < 3`, but the guard is called before the condition is checked. This is the only way to satisify the _guard rule_ when using a for-loop in C.

> 👍  The Guard Rule
>
> A call to `_g` (_the guard function_) is must be the first branch instruction after a loop instruction.

Below appears the webassembly output when the above is compiled. Note the guard function being called at the start of the loop. The only instructions allowed before this call are non-branch instructions (typically manipulating constants.)

```
    block  ;; label = @1
      loop  ;; label = @2
        i32.const 3
        i32.const 14
=====>  call $_g          <=====
        drop
        ...
```

### Nested Loops

When using nested loops the `maxiter` argument must reflect the total number of times the guard will be _hit_. This means you must multiply the nestings together.

Consider the example below:

```c
#define GUARD(maxiter) _g(__LINE__, (maxiter)+1)
for (int i = 0; GUARD(3), i < 3; ++i)
{
  for (int j = 0; GUARD(15), j < 5; ++j)
  {
    ...
  }
}
```

Notice the inner-loop's guard is set to **15**. You must multiply the loops together to compute the maximum number of times an inner guard will be hit during Hook execution.

### No recursion

Calls to non-Hook API functions are disallowed in the Hooks ammendment. All user code must fit within the two allowed Hook functions `cbak` and `hook`.

> ❗️ Warning
>
> Failure to use guards correctly will cause an attempted `SetHook` transaction to be rejected.
