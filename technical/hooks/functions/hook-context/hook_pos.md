---
description: Returns the position in the hook chain the currently executing hook occupies
---

# hook\_pos

### Behaviour

* Returns the position in the hook chain the currently executing hook occupies

### Definition

C

```c
int64_t hook_pos (void);
```

### Example

C

```c
int64_t pos = 
  	hook_pos();
```

### Parameters

This API has no parameters

### Return Code

| Type     | Description                                                                               |
| -------- | ----------------------------------------------------------------------------------------- |
| int64\_t | The position in the chain the currently executing hook occupies. The first position is 0. |
