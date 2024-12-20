---
description: Index into a slotted object and assign a sub-object to another slot
---

# slot\_subfield

### Behaviour

* Look up the object in slot `parent_slot`
* Retrieve the sub-object at `field_id`
* Place sub-object into the slot `new_slot` or the next available slot if `new_slot` is 0.
* Return the new slot number.

### Definition

C

```c
int64_t slot_subfield (
    uint32_t parent_slot,
  	uint32_t field_id,
  	uint32_t new_slot
);
```

### Example

C

```c
int64_t amt_slot = 
  	slot_subfield(oslot, sfAmount, 0);
```

### Parameters

| Name         | Type      | Description                                                                                                                                                                                                                                                                                                                                                                                                |
| ------------ | --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| parent\_slot | uint32\_t | Slot the parent object is in                                                                                                                                                                                                                                                                                                                                                                               |
| field\_id    | uint32\_t | <p>The <code>sf</code> code of the field you are searching for.<br><br>To compute this manually take the serialized <code>type</code> and shift it into the 16 highest bits of uint32_t, then take the <code>field</code> and place it in the 16 lowest bits.<br><br>For example:<br><code>sfEmitNonce</code> has <code>type</code> 5 and <code>field</code> 11 thus its value is <code>0x050BU</code></p> |
| new\_slot    | uint32\_t | New slot number to place the object from the selected field into. If null, choose the next available slot. _May be null._                                                                                                                                                                                                                                                                                  |

### Return Code

| Type     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The slot number of the newly allocated object<br><br>If negative, an error:<br><br><code>DOESNT_EXIST</code><br>- The searched for field isn't present in the parent slot or the parent slot is unfilled.<br><br><code>NO_FREE_SLOTS</code><br>- The API would require a new slot to be allocated but the Hook is already at the maximum number of slots.<br><br><code>INVALID_FIELD</code><br>- The specified field is not a valid <code>sf</code> field.<br><br><code>NOT_AN_OBJECT</code><br>- The slotted object is not a valid STObject.</p> |
