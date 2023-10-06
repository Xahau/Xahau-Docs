# URIToken

[\[Source\]](https://github.com/ripple/rippled/blob/master/src/ripple/protocol/impl/LedgerFormats.cpp#L157-L170)

_(Added by the \[URI Token amendment]\[].)_

A `URIToken` object describes a URI token, which can be used to represent a unique resource identifier in the ledger.

#### Example JSON

```json
{
  "Account": "rUn84CUYbNjRoTQ6mSW7BVJPSVJNLb1QLo",
  "OwnerNode": "0000000000000000",
  "Issuer": "rfkE1aSy9G8Upk4JssnwBxhEv5p4mn2KTy",
  "URI": "https://example.com/resource",
  "Digest": "46060241FABCF692D4D934BA2A6C4427CD4279083E38C77CBE642243E43BE291",
  "Amount": "100000000",
  "Destination": "rUn84CUYbNjRoTQ6mSW7BVJPSVJNLb1QLo",
  "PreviousTxnID": "5463C6E08862A1FAE5EDAC12D70ADB16546A1F674930521295BC082494B62924",
  "PreviousTxnLgrSeq": 6,
  "LedgerEntryType": "URIToken",
  "index": "49647F0D748DC3FE26BDACBC57F251AADEFFF391403EC9BF87C97F67E9977FB0"
}
```

#### Fields

A `URIToken` object has the following fields:

| Field               | JSON Type | \[Internal Type]\[] | Required? | Description                                                                                                                   |
| ------------------- | --------- | ------------------- | --------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `Account`           | String    | Account             | Yes       | The owner of the URI Token.                                                                                                   |
| `OwnerNode`         | String    | UInt64              | Yes       | A hint indicating which page of the owner's directory links to this object, in case the directory consists of multiple pages. |
| `Issuer`            | String    | Account             | Yes       | The issuer of the URI Token.                                                                                                  |
| `URI`               | String    | VL                  | Yes       | The URI represented by this token.                                                                                            |
| `Digest`            | String    | Hash256             | No        | Arbitrary 256-bit hash provided by the owner as a specific identifier for this URI Token.                                     |
| `Amount`            | String    | Amount              | No        | The amount of the URI Token.                                                                                                  |
| `Destination`       | String    | Account             | No        | The intended recipient of the URI Token.                                                                                      |
| `PreviousTxnID`     | String    | Hash256             | Yes       | The identifying hash of the transaction that most recently modified this object.                                              |
| `PreviousTxnLgrSeq` | Number    | UInt32              | Yes       | The index of the ledger that contains the transaction that most recently modified this object.                                |
| `LedgerEntryType`   | String    | UInt16              | Yes       | The value `0x0073`, mapped to the string `URIToken`, indicates that this object is a URI Token object.                        |

#### URI Token ID Format

The ID of a `URIToken` object is the \[SHA-512Half]\[] of the following values, concatenated in order:

* The URI Token space key (`0x0055`)
* The AccountID of the owner of the URI Token
* The URI represented by the URI Token
