---
description: What to expect when your Hook runs.
---

# Hook Fees

### Hook Creation Fees

SetHook transactions are charged per byte of created webassembly. The rate is 10000 drops per byte. Thus a 1kib Hook will cost 10 XAH to create.

### Hook Execution Fees

When Hooks are [Strongly Executed](weak-and-strong.md) the originating transaction must pay for the Strong Executions in the originating transaction's fee.

Hook Execution fees are charged at a rate of 1 drop per web assembly instruction in the worst-case execution of the function `hook` (or `cbak` in the case of a callback). Thus a small Hook with a lot of looping may end up attracting high runtime fees.

### Fee RPC Helper

Transaction fees on a ledger with the Hooks Amendment enabled become non-trivial to compute for end-users and/or wallet applications. This is because strong hooks must be paid for by the originator of a transaction, and there may be as many as 4 strong hooks on the sending account and 4 on the receiving account, as well as any other strong transactional stakeholders involved (as can be the case with some exotic transaction types). Further, if the transaction is a SetHook then the size of the parameters, the size of the code and whether it is a _create_ operation or an _install_ operation all determine the size of the fee.

Therefore it is highly recommended that **all** transactions be run through the updated fee RPC call before they are submitted to the ledger.

To invoke the RPC call:

1. Open a websocket connection to the Hooks node you will be working with.
2. Compose the serialized transaction you wish to know the fee for with the following:

* `Fee: "0"`
* `SigningPubKey: ""` (That is: 0 byte VL of type 0x73. In hex:`0x7300`.)
* Do **not** sign the transaction.

3. Submit it as a hex blob to the RPC as follows:

```json
{"command":"fee", "tx_blob":"<hex blob>"}
```

For HTTP POST RPC submit it as follows:

```json
{"method":"fee", "params": [{"tx_blob":"<hex blob>"}] }
```

The response should look something like

```json
{
  result: {
    drops: {
      base_fee: '130520',
    },
  //...
  },
  type: 'response'
}
```

Take the base fee and set it as the `Fee` field in the transaction. Now sign and submit it as per the normal transaction submission process.

If there is an invalid value for `tx_blob` or `tx_blob` is missing, a regular JSON result will be returned with a `base_fee` of 10.

### Emission Fees

Hooks have access to the same computation the _Fee RPC Helper_ does. To use this simply call [etxn\_fee\_base](../technical/hooks-c-functions/emitted-transaction/etxn_fee_base.md) with a buffer containing the serialised transaction as the arguments. As with the RPC call, you must ensure that the `Fee` field is present in the serialised transaction. The value is irrelevant.

When `etxn_fee_base` returns the recommended fee you may use [sto\_emplace](../technical/hooks-c-functions/serialization/sto_emplace.md) to emplace it into the serialised transaction before emission. The relevant field is `sfFee`.
