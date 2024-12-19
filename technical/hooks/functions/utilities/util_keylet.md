---
description: Compute a serialized keylet of a given type
---

# util\_keylet

### Concepts

* [Slots and Keylets](../../concepts-and-docs/slots-and-keylets.md)

> ### 📘Tip
>
> Not every Keylet type is supported by this utility function. If you need another Keylet type you can derive it yourself using [util\_sha512h](https://xrpl-hooks.readme.io/reference/util_sha512h) and by checking the required fields [here](https://github.com/XRPLF/rippled/blob/develop/src/ripple/protocol/impl/Indexes.cpp). A further Keylet tool may [assist you.](https://richardah.github.io/xrpl-keylet-tools/)

### Behaviour

* Compute a keylet of the specified `keylet_type` according to the parameters `a` through `f` depending on type.
* Write the serialized 34 byte keylet into `write_ptr`

### Definition

C

```c
int64_t util_keylet (
    uint32_t write_ptr,
    uint32_t write_len,
    uint32_t keylet_type,
    uint32_t a,
    uint32_t b,
    uint32_t c,
    uint32_t d,
    uint32_t e,
    uint32_t f
);
```

### Example

C

```c
uint8_t keylet[34];
if (util_keylet(keylet, 34, KEYLET_LINE,
              hook_accid, 20,
              account_field, 20,
              currency_code, 20) != 34)
	rollback("Keylet Failed.", 14, 1);
```

### Parameters

<table><thead><tr><th width="155">Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td>write_ptr</td><td>uint32_t</td><td>Pointer to a buffer the serialized keylet will be written to</td></tr><tr><td>write_len</td><td>uint32_t</td><td>Length of output buffer, should be at least 34.</td></tr><tr><td>keylet_type</td><td>uint32_t</td><td>One of the keylet types as defined in <code>hookapi.h</code> e.g. <code>KEYLET_LINE</code> for a trustline.</td></tr><tr><td>a</td><td>uint32_t</td><td>See keylet table below</td></tr><tr><td>b</td><td>uint32_t</td><td>See keylet table below</td></tr><tr><td>c</td><td>uint32_t</td><td>See keylet table below</td></tr><tr><td>d</td><td>uint32_t</td><td>See keylet table below</td></tr><tr><td>e</td><td>uint32_t</td><td>See keylet table below</td></tr><tr><td>f</td><td>uint32_t</td><td>See keylet table below</td></tr></tbody></table>

### Keylet Table

| Keylet Type                                                                          | Parameters                                                                                                                                                                                                                                                                                                                                                                   |
| ------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| KEYLET\_HOOK\_STATE                                                                  | <p><code>a</code> points to an Account ID<br><code>b</code> is the length of the Account ID (should be 20)<br><code>c</code> points to a hook state key<br><code>d</code> is the length of the key (should be 32)<br><code>e</code> points to a hook state namespace<br><code>f</code> is the length of the namespace (should be 32)</p>                                     |
| <p>KEYLET_AMENDMENTS<br>KEYLET_FEES<br>KEYLET_NEGATIVE_UNL<br>KEYLET_EMITTED_DIR</p> | `a`, `b`, `c`, `d`, `e`, `f` must all be zero                                                                                                                                                                                                                                                                                                                                |
| KEYLET\_SKIP                                                                         | <p>Either:<br><code>a</code>, <code>b</code>, <code>c</code>, <code>d</code>, <code>e</code>, <code>f</code> all zero<br>Or:<br><code>a</code> is a <code>LedgerIndex</code><br><code>b</code> is 1<br><code>c</code>, <code>d</code>, <code>e</code>, <code>f</code> must all ​be zero</p>                                                                                  |
| KEYLET\_LINE                                                                         | <p><code>a</code> points to the High Account ID<br><code>b</code> is the length of the above (should be 20)<br><code>c</code> points to the Low Account ID<br><code>d</code> is the length of the above (should be 20)<br><code>e</code> points to the Currency Code<br><code>f</code> is the length of the above (should be 20)</p>                                         |
| KEYLET\_QUALITY                                                                      | <p><code>a</code> points to a serialized keylet<br><code>b</code> is the length of the above (should be 34)<br><code>c</code> is the high 32 bits of the uint64 to pass<br><code>d</code> is the low 32 bits of the uint64 to pass<br><code>e</code>, <code>f</code> must all be zero</p>                                                                                    |
| KEYLET\_DEPOSIT\_PREAUTH                                                             | <p><code>a</code> points to an Account ID<br><code>b</code> is the length (should be 20)<br><code>c</code> points to an Account ID<br><code>d</code> is the length (should be 20)<br><code>e</code>, <code>f</code> must all be zero</p>                                                                                                                                     |
| <p>KEYLET_UNCHECKED<br>KEYLET_CHILD<br>KEYLET_EMITTED_TXN</p>                        | <p><code>a</code> points to a key.<br><code>b</code> is the length of the key (should be 32.)<br><code>c</code>, <code>d</code>, <code>e</code>, <code>f</code> must both ​be zero</p>                                                                                                                                                                                       |
| <p>KEYLET_OWNER_DIR<br>KEYLET_SIGNERS<br>KEYLET_ACCOUNT<br>KEYLET_HOOK</p>           | <p><code>a</code> points to an Account ID.<br><code>b</code> is the length (should be 20.)<br><code>c</code>, <code>d</code>, <code>e</code>, <code>f</code> must all be zero.</p>                                                                                                                                                                                           |
| KEYLET\_PAGE                                                                         | <p><code>a</code> points to a key.<br><code>b</code> is the length of the key (should be 32.)<br><code>c</code> is the high 32 bits of the uint64 to pass<br><code>d</code> is the low 32 bits of the uint64 to pass<br><code>e</code>, <code>f</code> must both ​be zero</p>                                                                                                |
| <p>KEYLET_OFFER<br>KEYLET_CHECK<br>KEYLET_ESCROW<br>KEYLET_NFT_OFFER</p>             | <p><code>a</code> points to an Account ID.<br><code>b</code> is the length (should be 20.)<br>And Either:<br><code>c</code> is a 32bit unsigned integer (sequence)<br><code>d</code> is 0<br>Or:<br><code>c</code> points to a 32 byte key<br><code>d</code> is the length of the key (32).<br>In both cases:<br><code>e</code> and <code>f</code> must be 0.</p>            |
| KEYLET\_PAYCHAN                                                                      | <p><code>a</code> points to an Account ID<br><code>b</code> is the length (should be 20)<br><code>c</code> points to an Account ID<br><code>d</code> is the length (should be 20)<br>And Either:<br><code>e</code> 32bit unsigned int to pass<br><code>f</code> is zero<br>Or:<br><code>e</code> points to a 32 byte key<br><code>f</code> is the length of the key (32)</p> |

### Return Code

| Type     | Description                                                                                                                                                                                                                                                                                                                                  |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The number of bytes written, should always be 34.<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.<br><br><code>INVALID_ARGUMENT</code><br>- Call didn't comply with the above table.<br><br><code>TOO_SMALL</code><br>- Writing buffer was smaller than 34 bytes.</p> |
