# Admin API Methods

These methods are intended exclusively for trusted personnel responsible for maintaining xahaud server operations.

### Key Generation Methods



| Method             | Description                                                                                                     |
| ------------------ | --------------------------------------------------------------------------------------------------------------- |
| validation\_create | Generate a formatted key pair for xhaud nodes. (Validators should use tokens instead of keys from this method.) |
| wallet\_propose    | Generate keys for a new account.                                                                                |

### Logging and Data Management Methods



| Method          | Description                                                     |
| --------------- | --------------------------------------------------------------- |
| can\_delete     | Enable online deletion of ledgers up to a specified ledger.     |
| download\_shard | Download a specific shard of ledger history.                    |
| ledger\_cleaner | Set up the ledger cleaner to detect and resolve corrupted data. |
| ledger\_request | Query a peer server for a specific ledger version.              |
| log\_level      | View or change log verbosity levels.                            |
| logrotate       | Reopen the log file.                                            |
| node\_to\_shard | Transfer data from the ledger store to the shard store.         |

### Server Control Methods

| Method         | Description                                       |
| -------------- | ------------------------------------------------- |
| ledger\_accept | Close and advance the ledger in stand-alone mode. |
| stop           | Shut down the xahaud server.                      |

### Signing Methods

| Method    | Description                           |
| --------- | ------------------------------------- |
| sign      | Cryptographically sign a transaction. |
| sign\_for | Contribute to a multi-signature.      |

### Peer Management Methods

| Method                   | Description                                        |
| ------------------------ | -------------------------------------------------- |
| connect                  | Force the server to connect to a specific peer.    |
| peer\_reservations\_add  | Add or update a reserved slot for a specific peer. |
| peer\_reservations\_del  | Remove a reserved slot for a specific peer.        |
| peer\_reservations\_list | View all reserved peer slots.                      |
| peers                    | Retrieve information about connected peers         |

### Status/Debugging Methods



| Method                 | Description                                                 |
| ---------------------- | ----------------------------------------------------------- |
| consensus\_info        | View the current state of the consensus process.            |
| feature                | Retrieve information about protocol amendments.             |
| fetch\_info            | Check the server’s synchronization status with the network. |
| get\_counts            | View statistics about server internals and memory usage.    |
| manifest               | Retrieve public key details for a known validator.          |
| print                  | Access information about internal subsystems.               |
| validator\_info        | Get the server's validator configuration details.           |
| validator\_list\_sites | View sites that publish validator lists.                    |
| validators             | Retrieve information about the current validators.          |
