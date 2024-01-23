---
description: An OfferCancel transaction removes an Offer object from Xahau.
---

# OfferCancel

\[[Source](https://github.com/Xahau/xahaud/blob/dev/src/ripple/app/tx/impl/URIToken.cpp)]

### Cancel with OfferSequence

```json
{
    "TransactionType": "OfferCancel",
    "Account": "ra5nK24KXen9AHvsdFTKHSANinZseWnPcX",
    "Fee": "12",
    "Flags": 0,
    "LastLedgerSequence": 7108629,
    "OfferSequence": 6,
    "Sequence": 7
}
```

### Cancel with OfferID

```json
{
    "TransactionType": "OfferCancel",
    "Account": "ra5nK24KXen9AHvsdFTKHSANinZseWnPcX",
    "Fee": "12",
    "Flags": 0,
    "LastLedgerSequence": 7108629,
    "OfferID": "49647F0D748DC3FE26BDACBC57F251AADEFFF391403EC9BF87C97F67E9977FB0",
    "Sequence": 7
}
```

### Fields

| Field           | JSON Type | \[Internal Type]\[] | Description                                                                                                                                                                                                                                               |
| --------------- | --------- | ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `OfferSequence` | Number    | UInt32              | _(Optional)_ The sequence number (or Ticket number) of a previous OfferCreate transaction. If specified, cancel any offer object in the ledger that was created by that transaction. It is not considered an error if the offer specified does not exist. |
| `OfferID`       | String    | Hash256             | _(Optional)_ The ID of the Offer ledger object to cancel, as a 64-character hexadecimal string.                                                                                                                                                           |

_Tip:_ To remove an old offer and replace it with a new one, you can use an \[OfferCreate transaction]\[] with an `OfferSequence` parameter, instead of using OfferCancel and another OfferCreate.

The OfferCancel method returns `tesSUCCESS` even if it did not find an offer with the matching sequence number.
