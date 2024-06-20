# TES Codes

The codes `tesSUCCESS`  and `tesPARTIAL` are the only codes that indicates a transaction succeeded. This does not always mean it accomplished what you expected it to do. (For example, an \[OfferCancel]\[] can "succeed" even if there is no offer for it to cancel.)&#x20;

The `tesPARTIAL` code indicates that a transaction has partially succeeded. Specifically, it is used in scenarios where an operation, such as deleting hook state records, exceeds a certain limit (e.g., 512 or 1024 records). In such cases, the transaction deletes up to the limit and then requires you to submit additional transactions with new sequence numbers to continue the deletion process until all records are removed. This ensures that large operations are broken down into manageable parts.

| Code         | Explanation                                                                                                                                               |
| ------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `tesSUCCESS` | The transaction was applied and forwarded to other servers. If this appears in a validated ledger, then the transaction's success is final.               |
| `tesPARTIAL` | The transaction partially succeeded and requires additional transactions to complete large operations, such as deleting more than a set limit of records. |
