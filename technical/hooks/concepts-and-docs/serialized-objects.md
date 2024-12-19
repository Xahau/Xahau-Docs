---
description: Manipulate raw serialized xahaud objects!
---

# Serialized Objects

### What are Serialized Objects?

The XRP Ledger has canonical [serialized](https://xrpl.org/serialization.html) forms of all objects subject to consensus. When writing a Hook it is inevitable you will come across serialized objects. These manifest as buffers containing what might appear to the developer as opaque binary blobs. In fact you can read these with the [XRPL-Binary-Visualiser](https://richardah.github.io/xrpl-binary-visualizer/).

For example an `sfAmount` field serializes to a collection of bytes like `61D50F26109A32B7EC`

### Serialized Object API

To assist Hook developers in working with serialized objects the `sto` namespace was created within the Hooks API. These functions manipulate pointers within a Hook-provided buffer. See table below.

| Hook API                                                    | at it does                                                                            |
| ----------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| [sto\_subfield](../functions/serialization/sto_subfield.md) | Index into a xrpld serialized object and return the location and length of a subfield |
| [sto\_subarray](../functions/serialization/sto_subarray.md) | Index into a xrpld serialized array and return the location and length of an index    |
| [sto\_emplace](../functions/serialization/sto_emplace.md)   | Emplace a field into an existing STObject at its canonical placement                  |
| [sto\_erase](../functions/serialization/sto_erase.md)       | Remove a field from an STObject                                                       |
| [sto\_validate](../functions/serialization/sto_validate.md) | Validate an STObject                                                                  |

Where applicable these APIs return an _offset_ and a _length_ encoded into a single int64\_t. See individual documentation for details.

### Example

At typical scenario in which you would use the STO API is in processing memos on an Originating Transaction. Since you will likely need access to the whole memo anyway, an efficient way to process a set of memos is simply to dump the whole `sfMemos` field into a buffer then index around within it. While it is also possible to use the slot API to do this by slotting the Originating Transaction it would result in additional code and additional copying.

```c
#define SUB_OFFSET(x) ((int32_t)(x >> 32))
#define SUB_LENGTH(x) ((int32_t)(x & 0xFFFFFFFFULL))
#define SBUF(str) (uint32_t)(str), sizeof(str)

uint8_t memos[2048];
int64_t memos_len = otxn_field(SBUF(memos), sfMemos);
for (int i = 0; GUARD(3), i < 3; ++i)
{
    int64_t memo_lookup = sto_subarray(memos, memos_len, i);
    if (memo_lookup < 0)
        rollback(SBUF("Memo lookup error"), 1);
    uint8_t*  memo_ptr = SUB_OFFSET(memo_lookup) + memos;
    uint32_t  memo_len = SUB_LENGTH(memo_lookup);
    // the above now point at the memo ... do something here
}
```

### Overlap with slots

You may notice some overlap between slot APIs and STO APIs. The key difference here is who _owns_ the underlying data:

* If you are using _slots_ then xrpld owns the object you are interacting with.
* If you are using the _STO API_ then the **Hook** owns the buffer you are interacting with.

Both sets of functions index into a Serialized Object without unnecessary copying.
