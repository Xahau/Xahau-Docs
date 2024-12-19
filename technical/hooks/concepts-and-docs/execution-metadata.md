---
description: What to expect when your Hook runs.
---

# Execution Metadata

When Hooks execute they leave behind information about the status of that execution. This appears in the Originating Transaction metadata as an `sfHookExecutions` block. This block contains the following fields:



| Field                  | Description                                                                                                                                                  |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| sfHookResult           | <p>Hooks can end in three ways: <code>accept</code>, <code>rollback</code> and <code>error</code>.<br>This is <em>not</em> the same as sfHookReturnCode!</p> |
| sfHookHash             | The SHA512H of the Hook at the time it was executed.                                                                                                         |
| sfHookAccount          | The account the Hook ran on.                                                                                                                                 |
| sfHookReturnCode       | The integer returned as the third parameter of `accept` or `rollback`.                                                                                       |
| sfHookReturnString     | The string returned in the first two parameters of `accept` or `rollback`, if any.                                                                           |
| sfHookInstructionCount | The total number of webassembly instructions that were executed when the Hook ran.                                                                           |
| sfHookEmitCount        | The total number of [Emitted Transactions](emitted-transactions.md) produced by the Hook.                                                                    |
| sfHookExecutionIndex   | The order in which the Hook was executed (as distinct from other Hook Executions on the same Originating Transaction.)                                       |
| sfHookStateChangeCount | The number of [Hook State](state-management.md) changes the Hook made during execution.                                                                      |
