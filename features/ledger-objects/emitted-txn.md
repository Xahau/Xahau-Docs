# Emitted Txn

_(Added by the \[Hooks amendment]\[].)_

An `EmittedTxn` object describes a transaction that has been emitted by a hook. The object contains all the fields of the original transaction, along with additional details about the emission.

### Example JSON

```json
{
  "Account": "rMPwD1b8dJUaqZHaBgEvFx4ENhtpPVvDsv",
  "Amount": "999999",
  "Destination": "rfCarbonVNTuXckX6x2qTMFmFSnm6dEWGX",
  "DestinationTag": 0,
  "EmitDetails": {
    "EmitBurden": "1",
    "EmitCallback": "rMPwD1b8dJUaqZHaBgEvFx4ENhtpPVvDsv",
    "EmitGeneration": 1,
    "EmitHookHash": "A9B5411F4A4368008B4736EEE47A34B0EFCBE74016B9B94CC6208FBC0BF5C0C2",
    "EmitNonce": "6B2A27D6864903A479614581A79D18E8C8ADCE01E3440C6E993BE07298ADC2A4",
    "EmitParentTxnID": "9763EB6B74AEF0F55F642243AD51F48490594434439002A6142E545E47318D56"
  },
  "Fee": "31",
  "FirstLedgerSequence": 7186113,
  "Flags": 2147483648,
  "LastLedgerSequence": 7186117,
  "Sequence": 0,
  "SigningPubKey": "000000000000000000000000000000000000000000000000000000000000000000",
  "SourceTag": 0,
  "TransactionType": "Payment"
}
```

### Fields

An `EmittedTxn` object has the following fields:

| Field             | JSON Type | \[Internal Type]\[] | Required? | Description                                                                                                                                                                                                                                              |
| ----------------- | --------- | ------------------- | --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `EmitDetails`     | Object    | Object              | Yes       | Contains details about the emission. This includes the generation of the emission, the burden of the emission, the callback address, the hash of the hook that emitted the transaction, the nonce of the emission, and the ID of the parent transaction. |
| `TransactionType` | String    | UInt16              | Yes       | The type of the transaction that was emitted.                                                                                                                                                                                                            |
| `Account`         | String    | Account             | Yes       | The account that emitted the transaction.                                                                                                                                                                                                                |
| `Fee`             | String    | Amount              | Yes       | The fee paid for the transaction.                                                                                                                                                                                                                        |
| `Sequence`        | Number    | UInt32              | Yes       | The sequence number of the transaction.                                                                                                                                                                                                                  |
| `SigningPubKey`   | String    | Blob                | Yes       | The public key that signs the transaction.                                                                                                                                                                                                               |

The `EmittedTxn` object also contains all the fields of the original transaction.

### EmitDetails Fields

An `EmitDetails` object has the following fields:

| Field             | JSON Type | \[Internal Type]\[] | Required? | Description |
| ----------------- | --------- | ------------------- | --------- | ----------- |
| `EmitGeneration`  | Number    | UInt32              | Yes       |             |
| `EmitBurden`      | String    | UInt64              | Yes       |             |
| `EmitParentTxnID` | String    | Hash256             | Yes       |             |
| `EmitNonce`       | String    | Hash256             | Yes       |             |
| `EmitCallback`    | String    | AccountID           | No        |             |
| `EmitHookHash`    | String    | Hash256             | Yes       |             |
