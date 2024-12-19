---
description: Inspect and manipulate on-ledger objects.
---

# Slots and Keylets

### Background

Xahau contains numerous heterogenous object types which a Hook has read-access to. For example: _transactions_, _accounts_, _ledgers_, and the subcomponents of each of these, to name just a few.

It is very easy to carelessly program a computer to do a lot of needless copy operations when disciplined access to the same underlying data (i.e. through a view) would suffice. The deliberate avoidance of copy operations in programming is referred to as [Zero copy](https://en.wikipedia.org/wiki/Zero-copy) in programming.

With Hooks the same principle applies. We want to avoid copying where possible. In particular we want to avoid as much as possible needlessly copying large objects such as whole ledgers, we also want to avoid serializaing and unserializing these where possible.

### What are slots?

Slots are part of the Hook API and provide a zero-copy _heterogenous_ access system for on-ledger objects and transactions.

* Each Hook has access to 255 slots during runtime.
* Each slot may be empty or may contain a _slotted_ object.
* The slot API allows traversal into inner objects, and allows these inner objects themselves to be slotted.
* The slot API allows slotted objects to be dumped to a buffer or otherwise read by the Hook.

The avilable slot APIs are:

| Hook API                                             | What it does                                                                           |
| ---------------------------------------------------- | -------------------------------------------------------------------------------------- |
| [slot](../functions/slot/slot.md)                    | Serialize and output a slotted object                                                  |
| [slot\_clear](../functions/slot/slot_clear.md)       | Free up a currently occupied slot                                                      |
| [slot\_count](../functions/slot/slot_count.md)       | Count the elements of an array object in a slot                                        |
| slot\_id                                             | Compute the canonical hash of the slotted object and return it                         |
| [slot\_set](../functions/slot/slot_set.md)           | Locate an object based on its keylet and place it into a slot                          |
| [slot\_subarray](../functions/slot/slot_subarray.md) | Index into a slotted array and assign a sub-object to another slot                     |
| [slot\_subfield](../functions/slot/slot_subfield.md) | Index into a slotted object and assign a sub-object to another slot                    |
| [slot\_type](../functions/slot/slot_type.md)         | Retrieve the field code of an object in a slot and, optionally, some other information |
| [slot\_float](../functions/slot/slot_float.md)       | Parse the STI\_AMOUNT in the specified slot and return it as an XFL enclosed number    |
| [slot\_size](../functions/slot/slot_size.md)         | Compute the serialized size of an object in a slot                                     |

### What are keylets?

Keylets are used to locate (point to) on-ledger objects. In brief they are a _hash_ of identifying information from the object, which is the canonical _handle_ for that object.

Hooks use a serialized 34 byte keylet format which can be derrived using the important [util\_keylet](ref:util_keylet) function. Without this looking up and slotting objects would be generally impossible.

> 🚧 Tip
>
> The Hook APIs which accept a 34 byte keylet will also generally accept a 32 byte canonical transaction hash.

### Example

In the following example a 34 byte keylet for a `signers` object is used to slot that object.

```c
uint8_t keylet[34];
if (util_keylet(SBUF(keylet), KEYLET_SIGNERS, SBUF(hook_accid), 0, 0, 0, 0) != 34)
    rollback(SBUF("Notary: Internal error, could not generate keylet"), 10);

// then requesting XRPLD slot that keylet into a new slot for us
int64_t slot_no = slot_set(SBUF(keylet), 0);
if (slot_no < 0)
   rollback(SBUF("Notary: Could not set keylet in slot"), 10);
```
