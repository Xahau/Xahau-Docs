# Collect Call

> 👍 Hook Design Philosophy
>
> Every party affected by a transaction should have the opportunity to have their hooks executed.

When hooks are not Strongly Executed it is unfair to bill the originating transaction for their execution. For example an _OfferCreate_ which crosses 20 offers on the DEX should not be forced to pay for the execution of each of those account's Hooks.

Therefore during typical Weak execution the fee for the execution is collected from the owner of the Hook. To enable this:

* The Hook owner must have set `asfTshCollect` on their Xahau account using the AccountSet transaction.
* The Hook owner must have set `hsfCollect` on the specific Hook they wish to be called as a Weak TSH.

### Fee Responsibility Table

| Type of Weak Execution                                                                                                                                                   | Fee                                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>Again As Weak</strong><br>- Happens when a Strongly Executed Hook calls <a href="../technical/hooks-functions/hook-context/hook_again.md">hook_again</a></p>  | Free (already paid by the Strong Execution).                                                                                                                                           |
| <p><strong>Callback</strong><br>- Happens when an emitted transaction either makes it into a ledger or is flagged as being impossible to ever make it into a ledger.</p> | Free (already paid during Emission).                                                                                                                                                   |
| <p><strong>Weak Transactional Stakeholder</strong><br>- Happens if a transaction in some way mildly affects your account.</p>                                            | Paid for by your account (not by the originating transaction) if and only if both your account is marked with `asfTshCollect` flag and your Hook is marked with the `hsfCollect` flag. |

> 🚧 Warning
>
> This is an advanced feature most Hook Developers will probably not use.
