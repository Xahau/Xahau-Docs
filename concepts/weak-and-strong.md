---
description: Which Hooks are allowed to run and when?
---

# Weak and Strong

> 👍 Hook Design Philosophy
>
> Every party affected by a transaction should have the opportunity to have their Hooks executed.

Transactional Stake Holders (TSH) are parties that somehow have a stake in or are otherwise affected by a transaction. Their particular stake may be a _weak_ or _strong_. The degree of connection with the transaction dictates whether the party has the right to have their Hooks executed and who has to pay for that execution.

For example:

* In a conventional direct XAH **Payment** transaction the two TSH are the _originating account_ and the _destination account_.
* In a **SetSignerList** transaction the TSH are the _originating account_ and each account whose address appears in the signer list, where such accounts are active on the ledger.
* In an **OfferCreate** transaction, other account's offers which are crossed by the originating transaction are all weak TSH and may opt for weak execution.

Due to the heterogenous nature of transactions on Xahau, TSH come in all shapes and sizes and can be exotic and non-intuitive. This becomes more true as time passes and more transaction types are added to the Ledger.

### Weak and Strong

Each TSH has either a weak or a strong connection to the transaction.

A **Strong** connection means:

1. The originating transaction must pay the fee for the execution of the TSH Hook Chain
2. The TSH has the right to rollback the whole transaction by calling `rollback()` from their Hook during execution.

A **Weak** connection means:

1. The originating transaction **does not** pay for the execution of the TSH Hook Chain.
2. The TSH pays for the execution of their own Hook Chain through a feature called [Collect Call Hooks](collect-call.md).
3. The TSH must have set an account flag `asfTshCollect` prior to the execution of the originating transaction.
4. The TSH **does not** have the right to rollback the whole transaction by calling `rollback()` from their Hook during execution (but can still modify their own Hook state and Emit transactions.)

### Before or After

Strong TSHes have their hooks executed _before_ the originating transaction is applied to the ledger. This means they have the ability to [rollback](../technical/hooks-functions/control/rollback.md) the transaction (because it hasn't yet been applied.) This gives strongly executed hooks the ability to completely block a transaction from occurring.

Weak TSHes have their hooks executed _after_ the originating transaction has been applied to the ledger. This means they have access to the [transaction metadata](../technical/hooks-functions/originating-transaction/meta_slot.md) but cannot prevent the transaction from occurring.

> 📘 Hint
>
> Strongly executed hooks can call [hook\_again](ref:hook_again) to be executed a second time as a weak execution after the originating transaction has been applied.

### Execution Context

The `uint32_t` parameter in `hook(uint32_t)` and `cbak(uint32_t)` carries important context information from the Hooks Amendment to your Hook.

During the execution of `hook`:

* 0 means the Hook is being executed _strongly_
* 1 means the Hook is being executed _weakly_
* 2 means the Hook is being executed _weakly_ after being executed _strongly_ due to a [hook\_again](../technical/hooks-functions/hook-context/hook_again.md) call.

During the execution of `cbak`:

* 0 means the Hook is being called back after a transaction it emitted was successfully accepted into a ledger.
* 1 means the Hook is being called back after a transaction it emitted was marked as never able to be applied to any ledger (EmitFailure).

### Reference Table

If a Transaction Type does not appear in the table then it has no TSHes **other than its originating account.**



| Transaction Type	       | TSH Type	     | Who is the TSH                                                                               |
| ----------------------- | ------------- | -------------------------------------------------------------------------------------------- |
| AccountDelete           | Strong        | Destination account funds are paid out to after deletion                                     |
| AccountSet              | None          | N/A                                                                                          |
| CheckCancel             | Weak          | Destination account                                                                          |
| CheckCash               | None          | N/A                                                                                          |
| CheckCreate             | Strong        | Destination account                                                                          |
| ClaimReward             | Strong        | Issuer Account                                                                               |
| DepositPreauth          | Strong        | Authorized account                                                                           |
| EscrowCancel            | Weak          | Destination account                                                                          |
| EscrowCreate            | Strong        | Destination account                                                                          |
| EscrowFinish            | Strong        | Destination account                                                                          |
| GenesisMint             | Weak          | Each Destination in the GenesisMints Array                                                   |
| Import                  | Strong        | Issuer Account                                                                               |
| Invoke                  | Strong        | Destination account                                                                          |
| OfferCancel             | None          | N/A                                                                                          |
| OfferCreate             | Weak          | Accounts whose offers were crossed by this action.                                           |
| Payment                 | Strong + Weak | Strong: Destination account. Weak: Any non-issuer the payment is rippled through.            |
| PaymentChannelClaim     | Weak          | Destination account                                                                          |
| PaymentChannelCreate    | Strong        | Destination account                                                                          |
| PaymentChannelFund      | Weak          | Destination account                                                                          |
| SetHook                 | None          | N/A                                                                                          |
| SetRegularKey           | Strong        | The account whose address is being set as the key.                                           |
| SignerListSet           | Strong        | Accounts whose addresses are set as signing keys (if they exist and have Hooks set on them). |
| TicketCreate            | None          | N/A                                                                                          |
| TrustSet                | Weak          | Issuer account                                                                               |
| URITokenCancelSellOffer | None          | N/A                                                                                          |
| URITokenCreateSellOffer | Strong        | Destination account, Issuer if tfBurnable Flag is set                                        |
| URITokenBurn            | Strong        | Issuer if tfBurnable Flag is set                                                             |
| URITokenBuy             | Strong        | Owner account, Issuer if tfBurnable Flag is set                                              |
| URITokenMint            | None          | N/A                                                                                          |

**AccountSet**

| OTXN    | TSH     | AccountSet |
| ------- | ------- | ---------- |
| Account | Account | Strong     |

**AccountDelete**

| OTXN    | TSH         | AccountDelete |
| ------- | ----------- | ------------- |
| Account | Account     | None          |
| Account | Beneficiary | Strong        |

**Check**

| OTXN        | TSH         | CheckCancel | CheckCreate | CheckCash |
| ----------- | ----------- | ----------- | ----------- | --------- |
| Account     | Account     | Strong      | Strong      | None      |
| Account     | Destination | Weak        | Strong      | None      |
| Destination | Destination | Strong      | None        | Strong    |
| Destination | Account     | Weak        | None        | Weak      |

**ClaimReward**

| OTXN    | TSH     | ClaimReward |
| ------- | ------- | ----------- |
| Account | Account | Strong      |
| Account | Issuer  | Strong      |

**DepositPreauth**

| OTXN    | TSH        | DepositPreauth |
| ------- | ---------- | -------------- |
| Account | Account    | Strong         |
| Account | Authorized | Strong         |

**Escrow**

| OTXN        | TSH         | EscrowCancel | EscrowCreate | EscrowFinish |
| ----------- | ----------- | ------------ | ------------ | ------------ |
| Account     | Account     | Strong       | Strong       | Strong       |
| Account     | Destination | Weak         | Strong       | Weak         |
| Destination | Destination | Strong       | None         | Strong       |
| Destination | Account     | Weak         | None         | Weak         |

**GenesisMint**

| OTXN    | TSH         | GenesisMint |
| ------- | ----------- | ----------- |
| Account | Account     | Strong      |
| Account | Destination | Strong      |
| Account | Beneficiary | Weak        |

**Import**

| OTXN    | TSH     | Import |
| ------- | ------- | ------ |
| Account | Account | Strong |
| Account | Issuer  | Strong |

**Invoke**

| OTXN    | TSH         | Invoke |
| ------- | ----------- | ------ |
| Account | Account     | Strong |
| Account | Destination | Weak   |

**Offer**

| OTXN    | TSH     | OfferCancel | OfferCreate |
| ------- | ------- | ----------- | ----------- |
| Account | Account | Strong      | Strong      |
| Account | Crossed | None        | Weak        |

**Payment**

| OTXN    | TSH         | Payment |
| ------- | ----------- | ------- |
| Account | Account     | Strong  |
| Account | Destination | Strong  |
| Account | Crossed     | Weak    |

**PaymentChannel**

| OTXN        | TSH         | PaymentChannelClaim | PaymentChannelCreate | PaymentChannelFund |
| ----------- | ----------- | ------------------- | -------------------- | ------------------ |
| Account     | Account     | Strong              | Strong               | Strong             |
| Account     | Destination | Weak                | Strong               | Weak               |
| Destination | Destination | Strong              | None                 | None               |
| Destination | Account     | Weak                | None                 | None               |

**SetHook**

| OTXN    | TSH     | SetHook |
| ------- | ------- | ------- |
| Account | Account | Strong  |

**SetRegularKey**

| OTXN    | TSH        | SetRegularKey |
| ------- | ---------- | ------------- |
| Account | Account    | Strong        |
| Account | RegularKey | Strong        |

**SignersListSet**

| OTXN    | TSH     | SignerListSet |
| ------- | ------- | ------------- |
| Account | Account | Strong        |
| Account | Signer  | Strong        |

**Ticket**

| OTXN    | TSH     | TicketCreate |
| ------- | ------- | ------------ |
| Account | Account | Strong       |

**TrustSet**

| OTXN    | TSH     | TrustSet |
| ------- | ------- | -------- |
| Account | Account | Strong   |
| Account | Issuer  | Weak     |

**URIToken**

| OTXN   | Burnable | TSH    | Mint   | Burn   | Buy    | Sell   | Cancel |
| ------ | -------- | ------ | ------ | ------ | ------ | ------ | ------ |
| Owner  | False    | Owner  | None   | Strong | Strong | Strong | Strong |
| Owner  | False    | Issuer | None   | Weak   | Weak   | Weak   | None   |
| Owner  | False    | Buyer  | None   | None   | None   | Strong | Weak   |
| Owner  | True     | Buyer  | None   | None   | None   | Strong | Weak   |
| Owner  | True     | Owner  | None   | Strong | Strong | Strong | Strong |
| Owner  | True     | Issuer | None   | Weak   | Strong | Strong | None   |
| Issuer | False    | Owner  | None   | None   | None   | None   | None   |
| Issuer | False    | Issuer | Strong | None   | None   | None   | None   |
| Issuer | False    | Buyer  | Weak   | None   | None   | None   | None   |
| Issuer | True     | Owner  | None   | Weak   | None   | None   | None   |
| Issuer | True     | Issuer | Strong | Strong | None   | None   | None   |
| Issuer | True     | Buyer  | Weak   | None   | None   | None   | None   |
| Buyer  | True     | Buyer  | None   | None   | Strong | None   | None   |
| Buyer  | True     | Owner  | None   | None   | Weak   | None   | None   |
