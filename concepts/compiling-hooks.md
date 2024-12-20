# Compiling Hooks

### Constraints

All Hooks are compiled to a single [webassembly module](https://webassembly.github.io/spec/core/syntax/modules.html) before they can be set onto an [Xahau account](https://xrpl.org/accounts.html).

A Hook always implements and exports exactly one or both of the following functions:

`int64_t hook(uint32_t ctx) { ... }` _required_

* Executed whenever a transaction comes into or leaves from the account the Hook is set on (`ctx = 0`) or
* Executed when executed as a [Weak Transactional Stakeholder](weak-and-strong.md) (`ctx > 0`).

`int64_t cbak(uint32_t ctx) { ... }` _optional_

* Executed when an emitted transaction is successfully accepted into a ledger (`ctx = 0`) or
* Executed when an emitted transaction cannot be accepted into any ledger (`ctx = 1`).

Hooks are not allowed to specify other functions. Instead they must make clever use of macros to do all their computation within these two functions. This is part of a computational restriction on hooks to keep their runtime predictable.

Additionally Hooks are afforded no _heap_ memory. All required memory must be reserved and used on the stack.

### Example

Here is an example Hook written in C. The Hook prints 0...3 to the trace log before accepting the originating transaction.

```c
#include <stdint.h>
#define GUARD(maxiter) _g(__LINE__, (maxiter)+1)
extern int32_t _g (uint32_t id, uint32_t maxiter);
extern int64_t accept (uint32_t read_ptr, uint32_t read_len, int64_t error_code);
extern int64_t trace_num (uint32_t read_ptr, uint32_t read_len, int64_t number);

int64_t hook(uint32_t ctx)
{
    for (int i = 0; GUARD(3), i < 3; ++i)
    {
        trace_num("test", 4, i);
    }
    accept (0,0,0); 
    return 0;
}
```

> 📘 Hint
>
> For educational purposes the above example deliberately does not include `hookapi.h` (which developers would typically use.)

### Compilation

A [variety of compilers](https://www.google.com/search?q=webassembly+compiler+C) will generate valid webassembly from a C source file. Once compiled, a Hook exists as a binary `.wasm` file. This contains a webassembly module. Using `wasmcc` to compile and the `wasm2wat` tool to convert to human readable webassembly this binary form can be rendered to the human readable form. Below appears the compilation result of the above example.

```
(module
  (type (;0;) (func (param i32 i32) (result i32)))
  (type (;1;) (func (param i32 i32 i64) (result i64)))
  (type (;2;) (func))
  (type (;3;) (func (param i32) (result i64)))
  (import "env" "_g" (func $_g (type 0)))
  (import "env" "trace_num" (func $trace_num (type 1)))
  (import "env" "accept" (func $accept (type 1)))
  (func $__wasm_call_ctors (type 2))
  (func $cbak (type 3) (param i32) (result i64)
    (local i32 i32 i32 i64)
    global.get 0
    local.set 1
    i32.const 16
    local.set 2
    local.get 1
    local.get 2
    i32.sub
    local.set 3
    i64.const 0
    local.set 4
    local.get 3
    local.get 0
    i64.store offset=8
    local.get 4
    return)
  (func $hook (type 3) (param i32) (result i64)
    (local i32 i32 i32 i32 i32 i32 i32 i32 i32 i32 i32 i32 i32 i32 i32 i32 i32 i64 i32 i32 i32 i64 i32 i32 i32)
    global.get 0
    local.set 1
    i32.const 16
    local.set 2
    local.get 1
    local.get 2
    i32.sub
    local.set 3
    local.get 3
    global.set 0
    i32.const 0
    local.set 4
    local.get 3
    local.get 0
    i64.store offset=8
    local.get 3
    local.get 4
    i32.store offset=4
    block  ;; label = @1
      loop  ;; label = @2
        i32.const 3
        local.set 5
        i32.const 14
        local.set 6
        i32.const 4
        local.set 7
        local.get 6
        local.get 7
        call $_g
        drop
        local.get 3
        i32.load offset=4
        local.set 8
        local.get 8
        local.set 9
        local.get 5
        local.set 10
        local.get 9
        local.get 10
        i32.lt_s
        local.set 11
        i32.const 1
        local.set 12
        local.get 11
        local.get 12
        i32.and
        local.set 13
        local.get 13
        i32.eqz
        br_if 1 (;@1;)
        i32.const 1024
        local.set 14
        i32.const 4
        local.set 15
        local.get 3
        i32.load offset=4
        local.set 16
        local.get 16
        local.set 17
        local.get 17
        i64.extend_i32_s
        local.set 18
        local.get 14
        local.get 15
        local.get 18
        call $trace_num
        drop
        local.get 3
        i32.load offset=4
        local.set 19
        i32.const 1
        local.set 20
        local.get 19
        local.get 20
        i32.add
        local.set 21
        local.get 3
        local.get 21
        i32.store offset=4
        br 0 (;@2;)
      end
    end
    i64.const 0
    local.set 22
    i32.const 0
    local.set 23
    local.get 23
    local.get 23
    local.get 22
    call $accept
    drop
    i32.const 16
    local.set 24
    local.get 3
    local.get 24
    i32.add
    local.set 25
    local.get 25
    global.set 0
    local.get 22
    return)
  (table (;0;) 1 1 funcref)
  (memory (;0;) 2)
  (global (;0;) (mut i32) (i32.const 66576))
  (global (;1;) i32 (i32.const 1029))
  (global (;2;) i32 (i32.const 1024))
  (global (;3;) i32 (i32.const 66576))
  (global (;4;) i32 (i32.const 1024))
  (export "memory" (memory 0))
  (export "__wasm_call_ctors" (func $__wasm_call_ctors))
  (export "__data_end" (global 1))
  (export "__global_base" (global 2))
  (export "__heap_base" (global 3))
  (export "__dso_handle" (global 4))
  (export "cbak" (func $cbak))
  (export "hook" (func $hook))
  (data (;0;) (i32.const 1024) "test\00"))
```

The average Hook developer will never need to examine webassembly directly. However it is a useful conceptual exercise to review the contents of the sample Hook.

Above we can see:

* Three functions are imported from the Hooks API (`_g`, `accept`, `trace_num`)
* Two functions are defined by the hook (`cbak`, `hook`)
* Two functions are exported by the hook (again: `cbak`, `hook`)
* Some static (constant) data is recorded in the hook (see `data` at the bottom).

It is very important to note that a Hook _must only_ import functions available to it from the Hooks API and _must_ only export the `cbak` and `hook` functions. In additional all hooks must import `_g` from the Hooks API, which is the `guard` function.

> 📘 Hint
>
> Webassembly is a platform-independent general computation `bytecode` language. It has a one-to-one mapping with a human readable equivalent. These are used interchangeably.

### Unwanted Exports

Most webassembly compilers (including the one above) produce additional exports for their own linking purposes. In many cases the generation of these is difficult or impossible to disable.

Unwanted exports will lead to an otherwise valid Hook being rejected. Therefore after compilation developers should use the [Hook Cleaner Utility](https://github.com/XRPLF/hook-cleaner-c) to strip out these out. Failure to do so will lead to your Hook being rejected.

> ❗️ Important
>
> Don't forget to use the [Hook Cleaner Utility](https://github.com/XRPLF/hook-cleaner-c) or your Hooks will be rejected.
