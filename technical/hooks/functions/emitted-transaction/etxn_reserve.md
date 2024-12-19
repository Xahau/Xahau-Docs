---
description: Estimate the required fee for a txn to be emitted successfully
---

# etxn\_reserve

### Concepts

* [Emitted Transactions](../../concepts-and-docs/emitted-transactions.md)

### Behaviour

* Specifies a number of emitted transactions this hook might emit during execution.

### Definition

C

```c
int64_t etxn_fee_base (
    uint32_t count
);
```

### Example

C

```c
int64_t result = 
    etxn_fee_base(2);
if (result < 2)
    rollback("Error reserving!", 16, 1);
```

### Parameters

| Name  | Type      | Description                                                                                 |
| ----- | --------- | ------------------------------------------------------------------------------------------- |
| count | uint32\_t | The largest number of transactions this hook might emit during the course of one execution. |

### Return Code

| Type     | Description                                                                                                                                                                                                                                                                                                                                                            |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The maximum number of emitted transactions this hook may emit. This will always be the same as the <code>count</code> parameter or an error as below.<br><br>If negative, an error:<br><code>ALREADY_SET</code><br>- The hook already called this function earlier.<br><br><code>TOO_BIG</code><br>- The specified number of emitted transactions is too large.</p> |
