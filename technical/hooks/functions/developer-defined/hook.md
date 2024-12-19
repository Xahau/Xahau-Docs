---
description: The main function of your hook
---

# hook

### Concepts

* [Compiling Hooks](../../concepts-and-docs/compiling-hooks.md)

### Behaviour

* `hook` is a user defined function called by `xahaud` in order to fire your hook.
* Your `hook` function calls either `accept` or `reject` to pass or reject the originating transaction.
* If execution reaches the end of the function it is implicitly an `accept`.

### Definition

C

```c
int64_t hook (
    uint32_t reserved
)
```

### Example

C

```c
int64_t hook(uint32_t reserved)
{
  return 0;
}
```

### Parameters

| Name     | Type      | Description              |
| -------- | --------- | ------------------------ |
| reserved | uint32\_t | Reserved for future use. |

### Return Code

| Type     | Description                                                                                                                      |
| -------- | -------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | An arbitrary return code you wish to return from your hook. This will be present in the metadata of the originating transaction. |
