---
description: Set the Hook State on another account for a given key, value and namespace
---

# state\_foreign\_set

### Behaviour

{% tabs %}
{% tab title="C" %}
* Read a 32 byte Hook State key from the `kread_ptr`
* Read an arbitrary amount of data from `read_ptr` (the value)
* Read a 32 byte Namespace from the `nread_ptr`
* Read a 20 byte Account ID from `aread_ptr`
* Update the Hook State key on the specified account within the specified namespace with the value
* But only if a [Grant](https://xrpl-hooks.readme.io/docs/grants) on that account allows this.
* If the Hook Account is specified in `aread_ptr` then the behaviour is that of state\_set but still allows specification of namespace through `nread_ptr`
{% endtab %}

{% tab title="Javascript" %}
* Sets the Foreign Hook State with the specified value, key, namespace, and account ID.
* This operation requires authorization and a Grant to allow this action.
* Returns the number of bytes written to Hook State (the length of the data), negative on error.
{% endtab %}
{% endtabs %}

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t state_foreign_set (
    uint32_t read_ptr,
    uint32_t read_len,
    uint32_t kread_ptr,
    uint32_t kread_len,
    uint32_t nread_ptr,
    uint32_t nread_len,
    uint32_t aread_ptr,
    uint32_t aread_len  
);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function state_foreign_set(
    value: ByteArray | HexString | undefined | null,
    key: ByteArray | HexString,
    namespace: ByteArray | HexString | undefined | null,
    accountid: ByteArray | HexString | undefined | null
  ): ErrorCode | number
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
#define SBUF(str) (uint32_t)(str), sizeof(str)
if (state_foreign_set(SBUF(vault), SBUF(vault_key), SBUF(namespace), SBUF(account)) < 0)
		rollback(SBUF("Error: could not set foreign state!"), 1);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
state_foreign_set(value, key, namespace, accountid)
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}
| Name       | Type      | Description                                                                                                                                              |
| ---------- | --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| read\_ptr  | uint32\_t | <p>Pointer to the data (value) to write into Hook State.<br>If this is <code>0</code> (null) then delete the data at this key. <em>May be null.</em></p> |
| read\_len  | uint32\_t | <p>The length of the data.<br>If this is <code>0</code> (null) then delete the data at this key. <em>May be null.</em></p>                               |
| kread\_ptr | uint32\_t | A pointer to the Hook State key at which to store the value.                                                                                             |
| kread\_len | uint32\_t | The length of the key. (Should always be 32.)                                                                                                            |
| nread\_ptr | uint32\_t | A pointer to the namespace which the key belongs to.                                                                                                     |
| nread\_len | uint32\_t | The length of the namespace. (Should always be 32.)                                                                                                      |
| aread\_ptr | uint32\_t | A pointer to the Account ID whose state we are trying to modify.                                                                                         |
| aread\_len | uint32\_t | The length of the Account ID. (Should always be 20.)                                                                                                     |

> ### 🚧Caution
>
> Xahau sets internally a maximum hook data size. At time of writing and for public testnet this is hard coded at 128 bytes, however in future it will be a validator-votable number.
{% endtab %}

{% tab title="Javascript" %}
| Name      | Type                   | Description                                     |
| --------- | ---------------------- | ----------------------------------------------- |
| value     | ByteArray or HexString | The value of data to persist.                   |
| key       | ByteArray or HexString | The key of the Hook State to set the value for. |
| namespace | ByteArray or HexString | The Hook namespace to look in.                  |
| accountid | ByteArray or HexString | The owner of the state.                         |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The number of bytes written to Hook State (the length of the data.)<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.<br><br><code>TOO_BIG</code><br>- <code>kread_len</code> was greater than 32, or<br>- <code>read_len</code> was greater than the maximum hook data size.<br><br><code>TOO_SMALL</code><br>- <code>kread_len</code> was 0.<br><br><code>NOT_AUTHORIZED</code><br>- no appropriate HookGrant was present on the foreign account to allow this state mutation.<br><br><code>PREVIOUS_FAILURE_PREVENTS_RETRY</code><br>- during this execution a previous <code>state_foreign_set</code> failed with NOT_AUTHORIZED, and consequently no further calls to this API are allowed during this execution.</p> |
{% endtab %}

{% tab title="Javascript" %}
| Type                | Description                                                                                    |
| ------------------- | ---------------------------------------------------------------------------------------------- |
| number or ErrorCode | Returns the number of bytes written to Hook State (the length of the data), negative on error. |
{% endtab %}
{% endtabs %}

