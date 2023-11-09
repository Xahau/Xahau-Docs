# Base 58 Encodings

Xahau APIs often use a "base58" encoding with a checksum (sometimes called "Base58Check") to represent account addresses and other types of values related to cryptographic keys. This encoding is the same as [the one used for Bitcoin addresses](https://en.bitcoin.it/wiki/Base58Check\_encoding), except that Xahau uses the following dictionary: `rpshnaf39wBUDNEGHJKLM4PQRST7VWXYZ2bcdeCg65jkm8oFqi1tuvAxyz`.

Xahau prefixes different types of values with a specific 8-bit number before encoding them to distinguish between different data types. With the arrangement of characters in Xahau's base58 dictionary, the result is that the base58 representations for different types of encoded values start with specific letters by type.

The following table lists all the encodings Xahau uses:

| Data Type                                | Starts With | Type Prefix | Content size¹ | Maximum characters |
| ---------------------------------------- | ----------- | ----------- | ------------- | ------------------ |
| Account address                          | r           | `0x00`      | 20 bytes      | 35                 |
| Account public key                       | a           | `0x23`      | 33 bytes      | 53                 |
| Seed value (for secret keys)             | s           | `0x21`      | 16 bytes      | 29                 |
| Validation public key or node public key | n           | `0x1C`      | 33 bytes      | 53                 |

¹ Content size excludes the 1-byte type prefix.

### See Also

* Address Encoding - detailed information on address encoding
* Cryptographic Keys - types of cryptographic keys in Xahau and how they're used
* \[wallet\_propose Reference]\[wallet\_propose method] - API method for generating account keys
* \[validation\_create Reference]\[validation\_create method] - API method for generating validator keys
