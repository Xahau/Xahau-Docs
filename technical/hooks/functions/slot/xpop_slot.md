---
description: Serialize and output the xpop transaction blob and metadata
---

# xpop\_slot

### Behaviour

* Locate the xpop blob on the `Import` transaction
* Emplace the located tx and meta objects into the slots specified

### Definition

C

```c
int64_t xpop_slot (
  	uint32_t slot_no_tx,
  	uint32_t slot_no_meta
);
```

### Example

C

```c
int64_t bytes_written = 
    xpop_slot(1, 2); // assumes a txn is slotted into slot=1 meta is slotted into slot=2
```

### Parameters

| Name           | Type      | Description                                    |
| -------------- | --------- | ---------------------------------------------- |
| slot\_no\_tx   | uint32\_t | The slot number to emplace the tx blob into.   |
| slot\_no\_meta | uin32\_t  | The slot number to emplace the meta blob into. |

### Return Code

| Type     | Description                                                                                                                                                                                                                                                |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p><code>PREREQUISITE_NOT_MET</code><br><br>- The originating tx type was not <code>Import</code>.<br><br><code>NO_FREE_SLOTS</code><br><br>- The API would require a new slot to be allocated but the Hook is already at the maximum number of slots.</p> |
