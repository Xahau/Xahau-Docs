---
description: Set the Hook State for a given key and value
---

# state\_set

### Behaviour

{% tabs %}
{% tab title="C" %}
* Read a 32 byte Hook State key from the `kread_ptr`
* Read an arbitrary amount of data from `read_ptr` (the value)
* Update the Hook State key with the value
{% endtab %}

{% tab title="Javascript" %}
* Sets the Hook State with the specified value and key.
* Returns the number of bytes written to Hook State (the length of the data), negative on error.
{% endtab %}
{% endtabs %}

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t state_set (
    uint32_t read_ptr,
    uint32_t read_len,
    uint32_t kread_ptr,
    uint32_t kread_len  
);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function state_set(
    value: ByteArray | HexString | undefined | null,
    key: ByteArray | HexString
  ): ErrorCode | number
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
#define SBUF(str) (uint32_t)(str), sizeof(str)
if (state_set(SBUF(vault), SBUF(vault_key)) < 0)
		rollback(SBUF("Error: could not set state!"), 1);
```

> ### 📘Hint
>
> To delete the state use `state_set(0, 0, SBUF(key);`.
{% endtab %}

{% tab title="Javascript" %}
```javascript
const result = state_set(vault, vault_key)
if (result < 0)
    rollback("Error: could not set state!", 1);
```

> ### 📘Hint
>
> To delete the state use `state_set(null, key);`.
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

> ### 🚧 Caution
>
> Xahaud sets internally a maximum hook data size. At time of writing and for mainnet this is hard coded at 256 bytes, however in future it will be a validator-votable number.
{% endtab %}

{% tab title="Javascript" %}
| Name  | Type                   | Description                                     |
| ----- | ---------------------- | ----------------------------------------------- |
| value | ByteArray or HexString | The value of data to persist.                   |
| key   | ByteArray or HexString | The key of the Hook State to set the value for. |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                                                                                                                                                                                                                                                                                             |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The number of bytes written to Hook State (the length of the data.)<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.<br><br><code>TOO_BIG</code><br>- <code>kread_len</code> was greater than 32, or<br>- <code>read_len</code> was greater than the maximum hook data size.<br><br><code>TOO_SMALL</code><br>- <code>kread_len</code> was 0.</p> |
{% endtab %}

{% tab title="Javascript" %}
| Type                | Description                                                                                    |
| ------------------- | ---------------------------------------------------------------------------------------------- |
| number or ErrorCode | Returns the number of bytes written to Hook State (the length of the data), negative on error. |
{% endtab %}
{% endtabs %}

