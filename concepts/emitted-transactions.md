---
description: Your Hook can do a lot more than just block or allow transactions!
---

# Emitted Transactions

### Background

**All** changes made to Xahau _must_ be the result of applying a valid transaction to the ledger. Thus if some change _X_ is made then some transaction _Y_ is responsible.

When designing the Hooks API we needed a way for Hooks to make changes to the ledger _beyond_ simply accepting or rejecting a transaction. However attaching these changes to the Originating Transaction was confusing and resulted in a large increase in the general complexity of the system.

Suppose for example that a Hook needs to send you some funds... the send operation would be effectively enacted onto the ledger by the Originating Transaction which might have been something completely unrelated such as an Account Set transaction. Additionally this send operation would need to be able to potentially trigger another Hook on the receiving end of a payment.

The solution: **Emitted Transactions**. We allow the Originating Transaction to do exactly what the contents of the Transaction say it will do. If our Hook needs to make an additional change to the ledger such as sending a payment, it creates and then _emits_ a brand new transaction.

### What are Emitted Transactions?

Emitted Transactions are _new_ transactions created by the execution of a Hook and entered into consensus for processing in the next ledger. The transaction may be of any Transaction Type but must follow strict emission rules.

To emit a transaction the Hook first prepares the serialized transaction then calls [emit](../technical/hooks-functions/emitted-transaction/emit.md).

Because emitted transactions can trigger Hooks in the next ledger which in turn may emit more transactions, all emitted transactions carry a `burden` and a `generation` field in their `EmitDetails` block. The `EmitDetails` block replaces the signature field in a traditional transaction.

The `burden` and `generation` fields collectively prevent [Fork bomb](https://en.wikipedia.org/wiki/Fork_bomb) attacks on the ledger by exponentially increasing the cost of exponentially expanding emtited transactions.

It is important to note that the Hooks API follows the strict rule of _no rewriting_. You _must_ present an emitted transaction in full, valid and canonically formed to xahaud for emission or it will be rejected. It is not xahaud's job to build your transaction for you. The Hook must do this itself.

### Callbacks

As introduced in [Introduction and Terminology](terminology.md) emitted transactions trigger callbacks when they are accepted into a ledger. Due to the decentralised nature of consensus acceptance into a ledger of an emitted transaction is **not a guarantee**, although it is usually all-but guaranteed.

If an emitted transaction expires before it can be accepted into a ledger (for any number of reasons: the ledgers may be full, the fee may be too high for the emitted transaction or the emitted transaction may be somehow invalid) then a _pseudo transaction_ is created in the ledger to clean up the emitted transaction. This pseudo transaction also calls the callback of your hook, with `parameter = 1` to indicate the emitted transaction indeed failed.

### Emission Rules

The [emit](../technical/hooks-functions/emitted-transaction/emit.md) Hook API will enforce the following rules on a proposed (to be emitted) transaction.

| # | Emission Rule                                          | Explanation                                                                                                                                                                                                                                              |
| - | ------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1 | `sfSequence` = 0                                       | Emitted Transactions _do not_ increase the sequence number of the Hook Account. This must always be set to zero.                                                                                                                                         |
| 2 | `sfPubSigningKey` = 0                                  | Emitted Transactions are not signed but this is a required field for xrpld processing. It must be set to all zeros.                                                                                                                                      |
| 3 | `sfEmitDetails` present and valid                      | Emitted Transactions require an `sfEmitDetails` block and this must be correctly filled. See EmitDetails section below.                                                                                                                                  |
| 4 | `sfSignature` absent                                   | This field must be absent in the emitted transaction because if it were not then the transaction would be ambiguous.                                                                                                                                     |
| 5 | `LastLedgerSequence` valid and in the future           | All emitted transactions must have a last ledger sequence set so that the Hook knows if the emitted transaction failed (since it did not get a callback in time). This is currently set to a maximum of 5 ledgers after the current ledger.              |
| 6 | `FirstLedgerSequence` valid and set to the next ledger | All emitted transactions must have a first ledger sequence set to the next ledger (after the current ledger) so that Hooks do not recursively cascade within a single ledger. This is currently enforced to be the next ledger after the current ledger. |
| 7 | Fee appropirately computed and set                     | The fee is dependent on the size of the emtited transaction and the burden on the network (i.e. whether this emitted transaction was the result of another emitted transaction.)                                                                         |
| 8 | Generation cap not exceeded                            | An emitted transaction can produce other emitted transactions, and these can form a chain. The length of the chain is the `sfEmitGeneration`. This is currently capped at 10.                                                                            |

### EmitDetails block

All emitted transactions must contain an `sfEmitDetails` object correctly populated with the fields in the table below.

| Field             | Required Value                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Description                                                                                                                                                                                                                                                                     |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| sfEmitGeneration  | <p>If the Originating Transaction was itself an emitted transaction then one more than the <code>sfEmitGeneration</code> of that transaction.<br><br>If the Originating Transaction was not an emitted transaction then <code>1</code>.<br><br>This should be populated using <a href="../technical/hooks-functions/emitted-transaction/etxn_generation.md">etxn_generation</a>.</p>                                                                                                                                                                  | This field keeps track of a chain of emitted transactions that in turn cause other transactions to be emitted.                                                                                                                                                                  |
| sfEmitBurden      | <p>If the Originating Transaction was itself an emitted transaction then the <code>burden</code> of the Originating Transaction multiplied by the maximum number of transactions the Hook has declared it will emit using <a href="../technical/hooks-functions/emitted-transaction/etxn_reserve.md">etxn_reserve</a>.<br><br>If the Originating Transaction was not an emitted transaction then <code>1</code>.<br><br>This should be populated using <a href="../technical/hooks-functions/emitted-transaction/etxn_burden.md">etxn_burden</a>.</p> | This field is a heuristic for detecting forkbombs. Fees are based on burden and will increase exponentially when a chain reaction is started to prevent the network becoming overun by self-reinforcing emitted transactions.                                                   |
| sfEmitParentTxnID | The transaction ID of the Originating Transaction                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | The Hook Execution that emitted the transaction is connected to the Originating Transaction. Therefore this field is always required for the efficient tracing of behaviour.                                                                                                    |
| sfEmitNonce       | A special deterministic nonce produced by a call to [nonce](../technical/hooks-functions/emitted-transaction/etxn_nonce.md)                                                                                                                                                                                                                                                                                                                                                                                                                           | Emitted Transactions would be identical with the same fields and therefore have identical transaction hashes if a nonce were not used. However every node on the network needs to agree on the nonce, so a special Hook API to produce a deterministic nonce is made available. |
| sfEmitCallback    | The 20 byte Hook Account ID                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | This field is used by xahaud when it needs to intitate a callback, such that it knows which Hook and account to initate the callback on. Callbacks happen when an emitted transaction is accepted into a ledger.                                                                |

> 👍 Check the examples
>
> The [Example Hooks](https://github.com/XRPL-Labs/xrpld-hooks/tree/hooks-ssvm/hook-api-examples), in particular Peggy, Carbon and Doubler, demonstrate how to emit both simple and more complicated transactions.
