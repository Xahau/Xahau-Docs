---
description: >-
  As Hooks-enabled networks require specific transaction fields & offer more
  transaction types, not all clients will work out of the box. `xrpl-accountlib`
---

# Transaction Signing

## Main differences

1. Hooks-enabled networks allow getting network definitions dynamically. Allowing clients to adapt available transaction types, ledger objects, properties, and value types. When implemented correctly, signing and encoding libraries don't have to be updated when the network adds transaction/object types/properties. <mark style="color:blue;">**The libraries below implement this and will handle this for you.**</mark>
2. Hooks-enabled networks require a **NetworkID** with every transaction to prevent transaction replay on another chain. The **NetworkID** will also be returned by a `server_info` RPC command in the `network_id` field (e.g. **`21338`** for Hooks V3 testnet)
3. Transactions on a Hooks-enabled network may need higher fees to deliver a transaction to another account, based on the Hooks that will be executed sending out of the sending account and receiving on the destination account. A reasonable fee to satisfy the Hooks execution can be dynamically fetched from a node by issuing the `fee` command while providing a transaction as `tx_blob`. <mark style="color:blue;">**The libraries below implement this and will handle this for you.**</mark>

## Javascript/Typescript

The [**npm package `xrpl-accountlib`**](https://www.npmjs.com/package/xrpl-accountlib) can sign transactions for Hooks-enabled networks, as it offers full dynamic network feature support fetching network definitions at runtime.

The [**npm package `xrpl-client`**](https://www.npmjs.com/package/xrpl-client) integrates nicely with `xrpl-accountlib` (and comes as a dependency) to dynamically fetch the aforementioned network definitions and account values, helping submit the transaction.

### Code Sample

```javascript
import {
  derive,
  utils,
  signAndSubmit,
} from "xrpl-accountlib"

const wss = 'wss://xahau-test.net'
const account = derive.familySeed("s...")

const networkInfo = await utils.txNetworkAndAccountValues(wss, account)

const tx = {
  TransactionType: "SetHook",
  Hooks: [ { Hook: {
    CreateCode: "0061736D01000000011C0460057F7F7F7F7F017E60037F7F7E017E60027F7F017F60017F017E02230303656E76057472616365000003656E7606616363657074000103656E76025F670002030201030503010002062B077F0141B088040B7F004180080B7F0041A6080B7F004180080B7F0041B088040B7F0041000B7F0041010B07080104686F6F6B00030AC4800001C0800001017F230041106B220124002001200036020C41920841134180084112410010001A410022002000420010011A41012200200010021A200141106A240042000B0B2C01004180080B254163636570742E633A2043616C6C65642E00224163636570742E633A2043616C6C65642E22",
    Flags: 1,
    HookApiVersion: 0,
    HookNamespace: "F".repeat(64),
    HookOn: "F".repeat(58) + "BFFFFE",
  }
  }],
  ...networkInfo.txValues,
  // ^^ This adds autmatically fetched values for you:
  // Sequence, Account, LastLedgerSequence,
  // Fee (Hooks enabled: autodetect (from ledger))
}

/**
 * Note: the code above and `signAndSubmit` results in automatically
 * fetching and setting a fee for you. If you want to check the fee
 * for min/max/..., get your own fee (string in drops) using:
 *    utils.networkTxFee(wss, tx)
 * 
 * e.g.
 *    const Fee = await utils.networkTxFee(wss, tx)
 *    assert(Number(Fee) < 50_000, "Auto fee above 50k drops, abort")
 *    Object.assign(tx, { Fee, })
 */

const submitted = await signAndSubmit(tx, wss, account)

console.log(submitted)
```
