---
description: >-
  The SetRemarks transaction enables accounts to attach, update, or remove
  arbitrary remarks (key-value pairs) on supported ledger objects.
---

# SetRemarks

\[[Source](https://github.com/Xahau/xahaud/blob/dev/src/ripple/app/tx/impl/SetRemarks.cpp)]

_(Added by the \[_&#x52;emarks _amendment]\[].)_

### Example

```json
{
  "TransactionType": "SetRemarks",
  "Account": "rWYkbWkCeg8dP6rXALnjgZSjjLyih5NXm",
  "Flags": 0,
  "ObjectID": "AABBCCDDEEFF00112233445566778899AABBCCDDEEFF00112233445566778899",
  "Remarks": [
    {
      "Remark": {
        "RemarkName": "CAFE",
        "RemarkValue": "DEADBEEF",
        "Flags": 0
      }
    }
  ]
}

```

| Field      | JSON Type | Internal Type | Description                                                                                    |
| ---------- | --------- | ------------- | ---------------------------------------------------------------------------------------------- |
| `Account`  | String    | AccountID     | The address of the account submitting the transaction (must be the owner/issuer of the object) |
| `ObjectID` | String    | Hash256       | The ledger object ID to which the remarks are attached (see Supported Objects)                 |
| `Remarks`  | Array     | Array         | Array of remark objects to set, update, or delete (see Remarks Format)                         |

### SetRemarks Flags

| Flag Name     | Hex Value    | Decimal Value | Description                                             |
| ------------- | ------------ | ------------- | ------------------------------------------------------- |
| `tfImmutable` | `0x00000001` | 1             | Marks the remark as immutable (cannot change or delete) |

### Remarks Format

Each entry in the `Remarks` array is an object with a single `Remark` field, which itself is an object with the following fields:

| Field         | JSON Type | Internal Type | Required | Description                                                              |
| ------------- | --------- | ------------- | -------- | ------------------------------------------------------------------------ |
| `RemarkName`  | String    | Blob          | Yes      | The name/key of the remark (1–256 bytes, must be unique per object)      |
| `RemarkValue` | String    | Blob          | No       | The value of the remark (1–256 bytes). Omit to delete the remark.        |
| `Flags`       | Number    | UInt32        | No       | Set to `1` (`tfImmutable`) to make the remark immutable. Default is `0`. |

### Supported Objects and Permissions

Remarks can be attached to the following ledger object types. **Only the specified party (owner or issuer) may create, update, or delete remarks on each object:**

| Ledger Object Type          | Who Can Set Remarks? | Notes                                                                                    |
| --------------------------- | -------------------- | ---------------------------------------------------------------------------------------- |
| **AccountRoot**             | Owner                | The account itself (the address in the object)                                           |
| **Offer**                   | Owner                | The account that created the offer                                                       |
| **Escrow**                  | Owner                | The account that created the escrow                                                      |
| **Ticket**                  | Owner                | The account that created the ticket                                                      |
| **PayChannel**              | Owner                | The account that created the payment channel                                             |
| **Check**                   | Owner                | The account that created the check                                                       |
| **DepositPreauth**          | Owner                | The account that created the deposit preauthorization                                    |
| **URI Token**               | Issuer               | The account that issued the URI token (field `sfIssuer`)                                 |
| **Trustline (RippleState)** | Issuer               | Only the issuer side of the trustline (the account that issued the IOU) can set remarks. |

### Limits

* **Maximum 32 remarks** per object.
* Each `RemarkName` and `RemarkValue` must be 1–256 bytes.
* Each `RemarkName` must be unique per object.
* Once a remark is marked as immutable (`Flags: 1`), it cannot be changed or deleted.

### Special Transaction Cost

The base transaction cost is increased by **1 drop per byte** of all `RemarkName` and `RemarkValue` fields in the transaction.

### Error Cases

| Error Code            | Description                                                                                  |
| --------------------- | -------------------------------------------------------------------------------------------- |
| `temDISABLED`         | The Remarks amendment is not enabled.                                                        |
| `temINVALID_FLAG`     | Invalid flags set on the transaction.                                                        |
| `temMALFORMED`        | The transaction is malformed (e.g., too many remarks, duplicate names, invalid field sizes). |
| `terNO_ACCOUNT`       | The sending account does not exist.                                                          |
| `tecNO_TARGET`        | The target object does not exist.                                                            |
| `tecNO_PERMISSION`    | The sender is not the owner/issuer of the object.                                            |
| `tecIMMUTABLE`        | Attempted to modify or delete an immutable remark.                                           |
| `tecTOO_MANY_REMARKS` | The number of remarks on the object would exceed the limit of 32.                            |



