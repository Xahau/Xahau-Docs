---
description: Avoid re-uploading the same bytecode to the ledger
---

# Reference Counted Hook Definitions

When a novel Hook's web assembly byte-code is uploaded to Xahau, a significant storage burden is imposed on the network. This storage burden is reflected in the [Hook Fees](hook-fees.md) charged by the network.

To avoid this burden (and high fees for end users) reference counting is used:

* The first time a novel Hook is installed, the [SetHook Transaction](sethook-transaction.md) must provide a significant fee.
* The Hook's web assembly byte-code becomes an unowned and reference counted object on the ledger (called a `HookDefinition`).
* Subsequent installations by the same or other users for an identical Hook (i.e. with identical byte-code) increment the reference count. These installations point at the same object on the ledger. These transactions are billed in a similar way to setting a Trust Line, as the storage burden for the Hook was already paid for in the original Set Hook transaction.
* While the reference count on the Hook Definition is greater than zero (meaning one or more accounts still have the Hook installed) the object remains on the ledger.

![](<../../../.gitbook/assets/spaces_m6f29os4wP16vCS4lHNh_uploads_TlDL7tsVNYi1yU64EZQh_3ef0cee-sethook-Page-2 (1).png>)
