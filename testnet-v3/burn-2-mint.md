---
description: >-
  Burn2Mint is a low-level inter-chain primitive and is intended for enterprise
  users to self-supply their own liquidity as needed for their own purposes.
---

# Burn 2 Mint

## Burn2Mint Technical Manual (Hooks V3 Testnet)

{% hint style="warning" %}
This process is deliberately non-trivial and is not designed for end users.\
\
**Burn2Mint is intended for use by liquidity providers only.**

_**This is a warning that will appear on the production version of this document. You may disregard it because you are burning free testnet XRP in this instance.**_
{% endhint %}

Burn2Mint is a low-level inter-chain primitive and is intended for enterprise users to self-supply their own liquidity as needed for their own purposes. Running your own nodes and performing this operation yourself on your own nodes means you and you alone bear responsibility for the outcome of the procedure.

The generation & collection of XPOPs fundamentally relies on collecting validation messages on the overlay network, which are ephemeral by nature. If your nodes are not reliably connected, or if your hardware, network connection or operating system fail at the wrong point in time, then the XPOP for a Burn Transaction might not be generated or might not be generated correctly. This can lead to loss of funds as the Burn Transaction's XPOP was not captured in time and it’s possible the validation messages are lost forever making a Mint Transaction impossible despite a successful Burn Transaction.

If you are not comfortable with taking these technical risks, or do not understand what you are doing, or are not an enterprise user, then please source your liquidity via other friendly friendly alternatives.

### Setup

To perform B2M, *two* XRPL protocol nodes should be operated by the user:

1. **Burn Node**, comprising:
   * A modified Rippled instance (modified to record XPOPs)
   * Universal linux binary here: [https://yidczxh.dlvr.cloud/pob](https://yidczxh.dlvr.cloud/pob)
   * [https://github.com/RichardAH/rippled/tree/proof-of-burn](https://github.com/RichardAH/rippled/tree/proof-of-burn)
   * Running a with a rippled.cfg that has:
     * an **\[xpop\_dir]** stanza specifying an output directory for generated XPOPs.
     * a **\[network\_id]** stanza specifying network\_id: 1
       * (in production this would be network 0)
     *   a `validators.txt` containing:\


         ```
         [validator_list_sites]
         https://vl.altnet.rippletest.net
         [validator_list_keys]
         ED264807102805220DA0F312E71FC2C69E1552C9C5790F6C25E3729DEB573D5860
         ```


2. **Mint Node**
   * In this test scenario you will connect directly to the V3 hooks testnet, you do not need to run your own node. In the production scenario you will need to run a Mint node, which is just a stock node for the target network. This is because public nodes will probably opt out of accepting Import transactions due to legal risk.
     * Connect to **wss://hooks-testnet-v3.xrpl-labs.com**
     * Or download [https://hooksv3d.xrpl-labs.com/hooksv3d.tar](https://hooksv3d.xrpl-labs.com/hooksv3d.tar)
       * And run with a config as described in [https://xumm.notion.site/Hooks-V3-staging-net-info-518fa261c5cd49d2bcb89a5b9e7bef05](https://www.notion.so/Hooks-V3-staging-net-info-518fa261c5cd49d2bcb89a5b9e7bef05?pvs=21)

## Technical Summary on B2M's procedure

#### New Transaction Type: `Import`

HooksV3 (_network\_id=21338_) introduces a new transaction type called _**Import**_, which accepts an XPOP from the Ripple testnet chain (_network\_id=1_) and provides for a “burn-to-mint” unidirectional value transfer and key / account synchronisation.

### Burn Transaction

A _**Burn Transaction**_ is a transaction that burns XRP on an a source XRPL chain, which would be used as proof (XPOP) to mint on a destination XRPL chain.

The following are supported transaction types:

* AccountSet
* SetRegularKey
* SignerListSet.

{% hint style="warning" %}

Tickets _**are not accepted**_ in **any** Burn Transactions and would lead to the Burn Transaction being invalid for minting. To protect from spam, transactions must be validated with real, natural sequence number.

{% endhint %}

Note that, other transaction types are not currently supported and cannot be used to mint on HooksV3. (However this may soon change.)

All three transactions types can be used for minting. This means the _**Fee**_ burned by the Burn Transaction is subsequently minted on HooksV3 after a successful `Import`.

If `SetRegularKey` or `SignerListSet` is used, then key synchronisation occurs according to the standard rules of the transaction type. If `AccountSet` is used, then no key synchronisation occurs on the destination XRPL chain (HooksV3).

A field called _**OperationLimit**_ must be present on the Burn Transaction to be the destination chain’s Network ID. This field is to prevent replay attacks on other B2M-integrated chains.

The Burn Transaction may be used for Minting if it has either a **tesSUCCESS** transaction code or _any_ of the **tec** transaction codes. Meaning, _if_ the fee was burnt, then the transaction can be used for minting. However key synchronisation _only_ occurs when the Burn Transaction result was tesSUCCESS.

Example Burn Transaction:

```json
{
	"TransactionType": "AccountSet",
	"Fee": 10000000,
	"OperationLimit": 21338
}
```

### XPOP Collection

Before submitting the Burn Transaction, ensure your Burn Node is synchronised with the testnet chain (Network ID: `1`).

After checking your Burn Node's state, submit the signed Burn Transaction to the Burn Node.

The Burn Node watches closed ledgers for transactions containing the **OperationLimit** field, and uses collected validation messages to generate an XPOP (Proof Of Burn). These are written to a file under the directory specified in **\[xpop\_dir]** stanza in the Burn Node’s `rippled.cfg`.

Wait for the ledger to close, then browse through the xpop\_dir for the Burn Transaction's XPOP according to its TXID. The file contains a JSON document, which is the XPOP that you'll be relaying to the destination XRPL chain (HooksV3).

Take the raw contents of this file and encode it as HEX. This will become the contents of the **Blob* field in the `Import` transaction.

### Mint Transaction

Your binary-codec will be missing the neccesary fields to construct the `Import` (Mint) transaction. If you are using ripple-binary-codec, you can update its `definitions.json` file in the following way:

1. Change directory into `node_modules`
2. Run `find . | grep 'dist/enums/definitions.json'` to locate the relevant file to update
3. Connect to **wss://hooks-testnet-v3.xrpl-labs.com**
4. Request: `{"command":"server_definitions"}`
5. Dump the contents of the `"result"` key into `definitions.json` from step 2.

The `Import` transaction type takes only one non-common field _**Blob.**_. This must contain the HEX encoded XPOP from the XPOP Collection phase.

* You can do this with `cat xpopjsonfile | xxd -p | tr -d '\n'`

The `Account` and `SigningPubKey` field (or Signers array) must match exactly between the Burn Transaction and the Mint Transaction. Users can only mint to the same account, which they burned from.

If the `Account` field specifies an account that does not yet exist on HooksV3, it will be created. In this case use 0 for the `Sequence` field on the Mint Transaction. If the account already exists on HooksV3, then use the next available Sequence number on the account on HooksV3.

Example Import:

```json
{
	"Account": "<same as it was in the Burn Transaction>",
	"TransactionType": "Import",
	"Blob": "<hex encoded (upper case) XPOP>",
	"Sequence": 0
} 
```

IMPORTANT: **The Mint Transaction must be signed exactly the same way and by the same account as the Burn Transaction!**

Encode and sign the transaction appropriately, yielding a signed transaction blob (hex).

If you are not running your own Mint node:

* Connect to **wss://hooks-testnet-v3.xrpl-labs.com**
* Submit the transaction to the node:

```json
{
	"command": "submit",
	"tx_blob": "<HEX ENCODED IMPORT TXN>"
}
```

Or, if you are running your own Mint node:

* Ensure the Mint Node is running and synchronised to Network ID 21338.
* Use the `submit` RPC call to submit the Mint Transaction.
  * You can do this from command-line using `./hooksv3d submit <hex here>`

### Considerations

If the Account is to be created on HooksV3 but the keying for the account is unclear from the context of the Burn Transaction, then the Account is created in a blackholed mode. It can be subsequently rekeyed using either keying transaction type.

If the Burn Transaction is either a `SignerListSet` or a `SetRegularKey` transaction, then provided it had a tesSUCCESS transaction result on the source XRPL chain (testnet), that same keying operation is now applied to that same account on the destination XRPL chain (HooksV3).

During testing, Accounts on HooksV3 _can_ be deleted, however on the production Hooks-enabled chain, they will not be able to be deleted.

Accounts on HooksV3 have an optional _**ImportSequence**_ field in the AccountRoot. If **Import** has ever been used on that account on HooksV3, this field is present and is populated with the most recently imported Burn Transaction’s Sequence number. This is to prevent replay attacks, but it also means that you should never submit your Burn2Mints out of sequence, otherwise the skipped transactions will never be accepted for Minting.
