# Ledger Data

Each ledger version in the XRP Ledger is made up of three parts:

* **Ledger Header**: Metadata about this ledger version itself.
* **Transaction Set**: All the transactions that were executed to create this ledger version.
* **State Data**: The complete record of objects representing accounts, settings, and balances as of this ledger version. (This is also called the "account state".)

### State Data

\{{ page\_children(pages|selectattr("html", "eq", "ledger-object-types.html")|first, 1, 1, True) \}}
