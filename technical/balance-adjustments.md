---
description: How to claim a Balance Adjustment on Xahau
---

# Balance Adjustments

### Opt-in + Claim

Opting into Balance Adjustments is the same transaction as claiming an adjustment. You must do this first to kick off the ability to claim later.

```
{
    "Account": "<rAddr...>",
    "TransactionType": "ClaimReward",
    "Issuer": "rHb9CJAWyB4rj91VRWn96DkukG4bwdtyTh",
    "NetworkID": 21337
}    
```

### Opt-out

To opt-out of Balance Adjustments, omit the Issuer field and set Flags to 1. Doing this will delete your average balance statistics. These will not be restored. If you opt-in again, they will be reset to a starting position.

```
{
    "Account": "<rAddr...>",
    "TransactionType": "ClaimReward",
    "NetworkID": 21337,
    "Flags" 1
} 
```

### Technical Details

Balance Adjustments are implemented as a combination of two pieces of code:

1. BalanceRewards Amendment (native code)
2. Genesis Account's Reward Hook (hook code).

BalanceRewards collect average balance statistics about the accounts they are activated on. These statistics are then passed to a target Hook when the user wishes to claim.

All interactions with this amendment are via the ClaimReward transaction:

<pre><code><strong>{
</strong>    "Account": "&#x3C;rAddr...>",
    "TransactionType": "ClaimReward",
    "Issuer": "rHb9CJAWyB4rj91VRWn96DkukG4bwdtyTh",
    "NetworkID": 21337
}    
</code></pre>

When a ClaimReward transaction is successfully submitted with a **tesSUCCESS** error code, the account's average balance statistics are reset. The only other thing the amendment does is invoke the Hooks on the specified Issuer's account.

The _Issuer_ field is the account responsible for fulfilling the claim. Depending on what's installed on the Issuer account, several things can happen:

* If no Hook is installed on the Issuer's account, then nothing is done, and the BalanceRewards statistics are simply reset.
* If a Hook is installed on the Issuer's account and the Hook performs a rollback, then the transaction fails, and the statistics are _not_ reset.
* If a Hook is installed on the Issuer's account and the Hook performs accept, then the transaction succeeds, and the statistics are reset. In this case, the Hook should also emit a transaction back to the user's account containing their reward.

In practice, on Xahau, the Issuer will probably always be the genesis account **rHb9CJAWyB4rj91VRWn96DkukG4bwdtyTh**.

Unless:

* Network Governance results in a different account being used for BalanceAdjustments.
* A non-Governance party runs its own BalanceRewards giveaway that the user wants to be involved with. Note that successful claims result in the average balance statistics being reset, so only one type of reward can be claimed per reset.

The average balance statistics exist as a collection of three new fields on the AccountRoot object. These are:

<table><thead><tr><th width="240">Field</th><th width="95.33333333333331">Type</th><th>Explanation</th></tr></thead><tbody><tr><td><code>sfRewardAccumulator</code></td><td>UINT64</td><td>The area under of the balance-time graph for your account since last ClaimReward transaction.</td></tr><tr><td><code>sfRewardLgrFirst</code></td><td>UINT32</td><td>The ledger number of the last ClaimReward transaction.</td></tr><tr><td><code>sfRewardLgrLast</code></td><td>UINT32</td><td>The ledger sequence number of the last transaction in or out of your account.</td></tr><tr><td><code>sfRewardTime</code></td><td>UINT32</td><td>The ledger time the last reward was claimed.</td></tr></tbody></table>



