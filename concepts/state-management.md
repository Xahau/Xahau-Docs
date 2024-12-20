---
description: Hooks can read and save small pieces of on-ledger data 🚀
---

# State Management

### What is Hook State?

[State](https://en.wikipedia.org/wiki/State_\(computer_science\)) in computer science describes information held by a system between executions (as distinct from inputs and outputs.) For example your browser leaves you logged in to a website even after you close and reopen it. The login cookie is held in the browser's _state_.

**Hook State** refers to a key-value mapping that logically exists for each account on Xahau whether or not any keys are currently present. The keys are always 32 bytes (unsigned 256 bit integer) and the values are variable length with a maximum size determined by validator voting, at time of writing 256 bytes.

State Management is achieved using

* [state](../technical/hooks-c-functions/state/state.md)
* [state\_set](../technical/hooks-c-functions/state/state_set.md)
* [state\_foreign](../technical/hooks-c-functions/state/state_foreign.md)

### Storing and fetching

The below example uses the [state\_set](../technical/hooks-c-functions/state/state_set.md) Hook API to assign the value `0xC001CAFE` to the key `0x0..000001` (uint256 = 1) in the Hook State of the Hook Account.

```c
uint8_t key[32] = {
    0x00U, 0x00U, 0x00U, 0x00U, 0x00U, 0x00U, 0x00U, 0x00U,
    0x00U, 0x00U, 0x00U, 0x00U, 0x00U, 0x00U, 0x00U, 0x00U,
    0x00U, 0x00U, 0x00U, 0x00U, 0x00U, 0x00U, 0x00U, 0x00U,
    0x00U, 0x00U, 0x00U, 0x00U, 0x00U, 0x00U, 0x00U, 0x01U
};
uint8_t value[4] = { 0xC0U, 0x01U, 0xCAU, 0xFEU };
if (state_set(value, 4, key, 32) == 4)
{
    // ... state successfully saved
}
```

In a subsequent Hook execution this value can now be retrieved using the same key:

```c
uint8_t value[4];
uint8_t key[32] = {
    0x00U, 0x00U, 0x00U, 0x00U, 0x00U, 0x00U, 0x00U, 0x00U,
    0x00U, 0x00U, 0x00U, 0x00U, 0x00U, 0x00U, 0x00U, 0x00U,
    0x00U, 0x00U, 0x00U, 0x00U, 0x00U, 0x00U, 0x00U, 0x00U,
    0x00U, 0x00U, 0x00U, 0x00U, 0x00U, 0x00U, 0x00U, 0x01U
};
if (state(value, 4, key, 32) < 0)
{
    // ... state fetch failed
}
```

After the above code has run the `value` buffer will be populated with the value found at the key.

> 📘 Hint
>
> The buffer `state()` reads into (writeptr) must be large enough to store the value currently held at that key. If it isn't the Hook API returns with a `TOO_SMALL` error.

### Foreign state

From time to time it may be advantageous for one Hook running on one account to read the Hook State of another Hook running on another account. The [state\_foreign](../technical/hooks-c-functions/state/state_foreign.md) Hook API does exactly this. Because the ledger is public there is no reasonable expectation of privacy anyway. Any Hook may therefore _read_ (but not write) the Hook State of any other Hook.

### Namespaces and querying

Please see [Namespaces](namespaces.md)
