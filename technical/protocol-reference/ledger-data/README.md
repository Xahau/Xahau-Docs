# Ledger Data

Each ledger version in the XRP Ledger is made up of three parts:

* **Ledger Header**: Metadata about this ledger version itself.
* **Transaction Set**: All the transactions that were executed to create this ledger version.
* **State Data**: The complete record of objects representing accounts, settings, and balances as of this ledger version. (This is also called the "account state".)

### State Data

Each ledger version's state data is a set of **ledger objects**, sometimes called _ledger entries_, which collectively represent all settings, balances, and relationships at a given point in time. To store or retrieve an object in the state data, the protocol uses that object's unique [**Ledger Object ID**](ledger-object-ids.md).

In the peer protocol, ledger objects have a [canonical binary format](../binary-format.md). In `rippled` APIs, ledger objects are represented as JSON objects.

A ledger object's data fields depend on the type of object; the XRP Ledger supports the following types:

* [Ledger Header](ledger-header.md)
* [Ledger Entry Common Fields](ledger-object-ids.md)
* [Ledger Entry Types](ledger-objects-types/)
