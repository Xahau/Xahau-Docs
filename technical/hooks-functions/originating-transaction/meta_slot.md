---
description: Load the metadata of the originating transaction into a slot
---

# meta\_slot

### Behaviour

* If the Hook is being [Weakly Executed](../../../concepts/weak-and-strong.md) then emplace the metadata of the originating transaction into the slot specified or into a new slot if no slot is specified

### Definition

C

```c
int64_t meta_slot (
  	uint32_t slot_no
);
```

### Example

C

```c
int64_t meta_slot_no = 
		meta_slot(0);
```

### Parameters

| Name     | Type      | Description                                                                   |
| -------- | --------- | ----------------------------------------------------------------------------- |
| slot\_no | uint32\_t | The slot number to emplace into, or 0 if you wish to pick the next available. |

### Return Code

| Type     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The slot the otxn was placed in<br><br><code>INVALID_ARGUMENT</code><br>- specified slot number exceeds the largest possible slot number<br><br><code>NO_FREE_SLOTS</code><br>- the request could not granted because no free slot was avaialble to place the originating transaction into.<br><br><code>PREREQUISITE_NOT_MET</code><br>- The hook is being <a href="../../../concepts/weak-and-strong.md">Strongly Executed</a> and therefore no transactional metadata is available.</p> |
