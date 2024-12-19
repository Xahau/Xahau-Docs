---
description: Specify which transaction types a Hook should be triggered on
---

# HookOn Field

### Understanding the HookOn field

Each bit in this unsigned 256-bit integer indicates whether the Hook should execute on a particular transaction type. All bits are _active low_ **except** bit 22 which is _active high_. Since 22 is ttHOOK\_SET this means the default value of all 0's will not fire on a SetHook transaction but will fire on every other transaction type. This is a deliberate design choice to help people avoid bricking their Xahau account with a misbehaving hook.

Bits are numbered from right to left:

* bit 0 - right most, i.e. the least significant bit.
* bit 63 - the left-most, i.e. the most significant bit.

Examples (assuming a 256-bit unsigned integer type):

1. If we want to completely disable the hook:

```c
~(1ULL << 22) /* every bit is 1 except bit 22 which is 0 */
```

2. If we want to disable the hook on everything except ttPAYMENT:

```c
~(1ULL << 22) & ~(1ULL)
```

3. If we want to enable the hook on everything except ttHOOK\_SET

```c
0
```

4. If we want to enable hook firing on ttHOOK\_SET (dangerous) and every other transaction type:

```c
(1ULL << 22)
```

### HookOn Calculator



{% embed url="https://richardah.github.io/xrpl-hookon-calculator/" %}
