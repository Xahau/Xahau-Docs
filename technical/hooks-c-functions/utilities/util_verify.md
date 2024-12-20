---
description: Verify a cryptographic signature
---

# util\_verify

### Behaviour

Verify a cryptographic signature

* If the public key is prefixed with `0xED` then use `ED25519`
* Otherwise assume `SECP256k1`

### Definition

C

```c
int64_t util_verify (
    uint32_t dread_ptr,
    uint32_t dread_len,
    uint32_t sread_ptr,
    uint32_t sread_len,
    uint32_t kread_ptr,
    uint32_t kread_len
);
```

### Example

C

```c
if (!util_verify(payload_ptr,    payload_len,
                 signature_ptr,  signature_len,
                 publickey_ptr,  publickey_len))
	rollback("Invalid Signature", 17, 60);
```

### Parameters

<table><thead><tr><th>Name</th><th width="117">Type</th><th>Description</th></tr></thead><tbody><tr><td>dread_ptr</td><td>uint32_t</td><td>Pointer to the signed data</td></tr><tr><td>dread_len</td><td>uint32_t</td><td>Length of the signed data</td></tr><tr><td>sread_ptr</td><td>uint32_t</td><td>Pointer to the signature</td></tr><tr><td>sread_len</td><td>uint32_t</td><td>Length of the signature</td></tr><tr><td>kread_ptr</td><td>uint32_t</td><td>Pointer to the public key</td></tr><tr><td>kread_len</td><td>uint32_t</td><td>Length of the public key</td></tr></tbody></table>

### Return Code

<table><thead><tr><th width="126">Type</th><th>Description</th></tr></thead><tbody><tr><td>int64_t</td><td><code>0</code> - validation failed, the signature is invalid.<br><code>1</code> - validation succeeded, the signature is valid.<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.</td></tr></tbody></table>
