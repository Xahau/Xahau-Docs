---
description: >-
  Xahau smart contracts (Hooks) need transaction & destination specific fees.
  You can easily get the required fee from the `fee` RPC command.
---

# Transaction Fees

While libraries may deal with fee determination for you (see [.](./ "mention")), when building your own integrations with the Xahauy ledger, you may have to implement dynamic fee determination based on the transaction, source & destination account.

As the sender of a transaction will have to pay for the fees required for the invoked Hooks for the specific transaction type, where Hooks can live both on the source & destination account, you can send a TX Blob (signed with a dummy account) to the `fee` command, after which Xahau will return the specific fees required for the specific transaction.

### Fee RPC Helper

Transaction fees on a ledger with the Hooks Amendment enabled become non-trivial to compute for end-users and/or wallet applications. This is because strong hooks must be paid for by the originator of a transaction, and there may be as many as 4 strong hooks on the sending account and 4 on the receiving account, as well as any other strong transactional stakeholders involved (as can be the case with some exotic transaction types). Further, if the transaction is a SetHook then the size of the parameters, the size of the code and whether it is a _create_ operation or an _install_ operation all determine the size of the fee.

Therefore it is highly recommended that **all** transactions be run through the updated fee RPC call before they are submitted to the ledger.

#### To invoke the RPC call:

1. Open a websocket connection to the Hooks node you will be working with.
2. Compose the serialized transaction you wish to know the fee for with the following:

* `Fee: 0`
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

{% hint style="success" %}
Source: [https://xrpl-hooks.readme.io/docs/hook-fees](https://xrpl-hooks.readme.io/docs/hook-fees)
{% endhint %}
