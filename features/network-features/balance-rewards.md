# Balance Rewards

The Balance Rewards feature is a unique aspect of the Xahau network that allows users to accumulate and claim rewards based on their account balance. This feature is implemented through a combination of native code (BalanceRewards Amendment) and hook code (Genesis Account's Reward Hook).

### Transaction Types

#### ClaimReward

A `ClaimReward` transaction allows an account to claim the rewards it has accumulated. The rewards can be claimed by the account owner or by a specified issuer. The account can also opt-out of rewards by setting the Flags field to 1.

{% content-ref url="../../technical/protocol-reference/transactions/transaction-types/claimreward.md" %}
[claimreward.md](../../technical/protocol-reference/transactions/transaction-types/claimreward.md)
{% endcontent-ref %}

#### GenesisMint

The `GenesisMint` transaction type is also associated with the Balance Rewards feature. This is an Emitted transaction that is executed through the Reward Hook every time a user claims balance rewards.

{% content-ref url="../../technical/protocol-reference/transactions/transaction-types/genesismint-emitted-txn.md" %}
[genesismint-emitted-txn.md](../../technical/protocol-reference/transactions/transaction-types/genesismint-emitted-txn.md)
{% endcontent-ref %}
