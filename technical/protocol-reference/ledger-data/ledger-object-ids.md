# Ledger Object IDs

[\[Source\]](https://github.com/ripple/rippled/blob/master/src/ripple/protocol/impl/Indexes.cpp)

Each object in a ledger's state data has a unique ID. The ID is derived by hashing important contents of the object, along with a [namespace identifier](https://github.com/ripple/rippled/blob/master/src/ripple/protocol/LedgerFormats.h#L99). The ledger object type determines which namespace identifier to use and which contents to include in the hash. This ensures every ID is unique. To calculate the hash, `xahaud` uses SHA-512 and then truncates the result to the first 256 bits. This algorithm, informally called **SHA-512Half**, provides an output that has comparable security to SHA-256, but runs faster on 64-bit processors.

Generally, a ledger object's ID is returned as the `index` field in JSON, at the same level as the object's contents. In transaction metadata, the ledger object's ID in JSON is `LedgerIndex`.

**Tip:** The `index` or `LedgerIndex` field of an object in the ledger is the ledger object ID. This is not the same as a \[ledger index]\[].

\{{ include\_svg("img/ledger-object-ids.svg", "Diagram: xahaud uses SHA-512Half to generate IDs for ledger objects. The space key prevents IDs for different object types from colliding.") \}}

### See Also

* For more information how Xahau creates and uses hashes, see Hashes.
* For ledger basics, see Ledgers.
