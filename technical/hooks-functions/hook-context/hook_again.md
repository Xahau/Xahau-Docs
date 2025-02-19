---
description: Returns the position in the hook chain the currently executing hook occupies
---

# hook\_again

### Behaviour

* If the hook is being strongly executed then flag this specific hook in the chain for [Again As Weak Execution](../../../concepts/weak-and-strong.md).
* If the originating transaction successfully is applied then the hook will be called again in a second, Weak Execution.

### Definition

C

```c
int64_t hook_again (void);
```

### Example

C

```c
int64_t result = 
  	hook_again();
```

### Parameters

This API has no parameters

### Return Code

<table><thead><tr><th width="176">Type</th><th>Description</th></tr></thead><tbody><tr><td>int64_t</td><td><code>1</code> iff successfully flagged for Again As Weak.<br><br><code>PREREQUISITE_NOT_MET</code><br>- This hook is already being executed weakly at the time of the call.<br><br><code>ALREADY_SET</code><br>- The function was already called this execution.</td></tr></tbody></table>
