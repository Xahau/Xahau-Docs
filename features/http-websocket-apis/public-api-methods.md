# Public API Methods

Interact directly with an xahaud server using public API methods. These methods are not necessarily intended for general public use but are accessible to any client connected to the server.&#x20;

### Account Methods



| Method              | Description                                                            |
| ------------------- | ---------------------------------------------------------------------- |
| account\_channels   | List payment channels where the account is the channel source.         |
| account\_currencies | List currencies the account can send or receive.                       |
| account\_info       | Retrieve basic information about an account.                           |
| account\_lines      | Access trust line information for an account.                          |
| account\_objects    | Retrieve all ledger objects owned by an account.                       |
| account\_offers     | View an account’s currency exchange offers.                            |
| account\_tx         | Retrieve transaction history for an account.                           |
| gateway\_balances   | Calculate total issued amounts for an account.                         |
| noripple\_check     | Suggest changes to an account's Default Ripple and No Ripple settings. |

### Ledger Methods



| Method          | Description                                        |
| --------------- | -------------------------------------------------- |
| ledger          | Get information about a specific ledger version.   |
| ledger\_closed  | Retrieve the most recently closed ledger version.  |
| ledger\_current | Retrieve the current working ledger version.       |
| ledger\_data    | Access raw ledger content.                         |
| ledger\_entry   | Retrieve a specific element from a ledger version. |

### Transaction Methods



| Method              | Description                                                |
| ------------------- | ---------------------------------------------------------- |
| submit              | Submit a transaction to the network.                       |
| submit\_multisigned | Submit a multi-signed transaction.                         |
| transaction\_entry  | Retrieve details about a transaction in a specific ledger. |
| tx                  | Retrieve transaction information across all ledgers.       |
| sign                | (Admin) Cryptographically sign a transaction.              |
| sign\_for           | (Admin) Contribute to a multi-signature.                   |

### Order Book Methods

| Method              | Description                                                 |
| ------------------- | ----------------------------------------------------------- |
| book\_offers        | View offers for exchanging two currencies.                  |
| deposit\_authorized | Check if one account can send payments directly to another. |

### Payment Channel Methods



| Method             | Description                               |
| ------------------ | ----------------------------------------- |
| channel\_authorize | Sign a claim for a payment channel        |
| channel\_verify    | Verify a payment channel claim signature. |

### Subscription Methods



| Method      | Description                     |
| ----------- | ------------------------------- |
| subscribe   | Listen for updates on a subject |
| unsubscribe | Stop receiving updates          |

### Server Info Methods

| Method        | Description                                   |
| ------------- | --------------------------------------------- |
| fee           | Retrieve information about transaction costs. |
| server\_info  | Get server status in human-readable format.   |
| server\_state | Get server status in machine-readable format. |
| manifest      | Retrieve public key details for a validator.  |

### Utility Methods



| Method | Description                                                            |
| ------ | ---------------------------------------------------------------------- |
| json   | Proxy for running commands with JSON parameters. _(Commandline only.)_ |
| ping   | Verify server connectivity.                                            |
| random | Generate random numbers.                                               |
