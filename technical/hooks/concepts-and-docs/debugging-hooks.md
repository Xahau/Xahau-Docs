---
description: How to print "hello world" from your Hook!
---

# Debugging Hooks

### How can I debug a Hook?

The Hook API provides a set of functions in the namespace `trace` which write output to the `xrpld` log file when xrpld is configured with the _trace_ log-level. These functions, generally speaking, allow you to see the value of variables, buffers and otherwise trace the execution and state of a Hook at runtime.

> 📘 Hint
>
> At time of writing there is no interactive Hook Debugger. You must use the trace functions.

### Trace APIs

The following `trace` functions are available in the Hooks API

| Hook API                                                | What it does                                                                              |
| ------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| [trace](../functions/trace-debug/trace.md)              | Print a utf-8 message, followed by a user-specified buffer (this last optionally as hex.) |
| [trace\_num](../functions/trace-debug/trace_num.md)     | Print a utf-8 message, followed by an integer.                                            |
| [trace\_float](../functions/trace-debug/trace_float.md) | Print a utf-8 message, followed by an XFL Floating point number.                          |
| trace\_slot                                             | Print a utf-8 message, followed by the serialized contents of a slot.                     |

### Example

The following code will print a single trace line then accept the Originating Transaction.

```c
#include "../hookapi.h"
int64_t hook(int64_t reserved)
{
  trace_num(SBUF("A number"), 10);
  accept(0,0,0);
  return 0;
}
```

An example of the log-line produced by `xahaud` when a payment is sent out of or into the Hook Account:

```
2021-Apr-13 13:59:11.083700726 UTC View:TRC
    HookTrace[rHb9CJAWyB4rj91VRWn96DkukG4bwdtyTh-rE3SfnjwfzZFL3JK9cLVfJuy8Ar1XnCqPw]:
        A number 10
```

The above appears in the log as all-one-line, but split here for visibility.

> 👍 Use testnet
>
> The [Xahau Testnet](https://xahau-test.net/) is the perfect place to test your Hooks.

### Log format

A breakdown of the log format appears in the table below

| Part                                        | Description                                                                                                                                                            | # |
| ------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | - |
| 2021-Apr-13 13:59:11.083700726 UTC View:TRC | `xahaud`'s prefix to the log line                                                                                                                                      | 1 |
| HookTrace                                   | This is a trace initiated by the Hook itself not some other information about the Hook. Other information is available on tags `HookError`, `HookEmit` and `HookInfo`. | 2 |
| \[rHb9CJAWyB4rj91VRWn96DkukG4bwdtyTh        | The first account in the square brackets is the Hook Account.                                                                                                          | 3 |
| -rE3SfnjwfzZFL3JK9cLVfJuy8Ar1XnCqPw]:       | The second account in the square brackets is the Originating Account.                                                                                                  | 4 |
| A number                                    | This is the message the Hook was told to deliver before the trace payload                                                                                              | 5 |
| 10                                          | This is the trace payload                                                                                                                                              | 6 |

> 🚧 Tip
>
> `Xahaud` produces a lot of output. It is therefore generally advisible to grep logs for the account/s you are interested in.\
> For example use: `tail -f log | grep HookTrace | grep <account>`
