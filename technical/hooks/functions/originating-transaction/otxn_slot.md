---
description: Load the originating transaction into a slot
---

# otxn\_slot

### Behaviour

* Emplace the originating transaction into the slot specified or into a new slot if no slot is specified

### Definition

C

```c
int64_t otxn_slot (
  	uint32_t slot_no
);
```

### Example

C

```c
int64_t otxn_slot_no = 
		otxn_slot(0);
```

### Parameters

| Name     | Type      | Description                                                                   |
| -------- | --------- | ----------------------------------------------------------------------------- |
| slot\_no | uint32\_t | The slot number to emplace into, or 0 if you wish to pick the next available. |

### Return Code

| Type     | Description                                                                                                                                                                                                                                                                                        |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The slot the otxn was placed in<br><br><code>INVALID_ARGUMENT</code><br>- specified slot number exceeds the largest possible slot number<br><br><code>NO_FREE_SLOTS</code><br>- the request could not granted because no free slot was avaialble to place the originating transaction into.</p> |
