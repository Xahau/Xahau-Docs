---
description: >-
  Retrieve the data pointed to by a Hook State key and write it to an output
  buffer
---

# state

### Behaviour

{% tabs %}
{% tab title="C" %}
* Read a 32 byte Hook State key from the `kread_ptr`
* Write the data (value) at that key to the buffer pointed to by `write_ptr`
{% endtab %}

{% tab title="Javascript" %}
* Retrieves the Hook State value associated with the specified key.
* Returns an error code or the Hook State value for the key.
{% endtab %}
{% endtabs %}

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t state (
    uint32_t write_ptr,
    uint32_t write_len,
    uint32_t kread_ptr,
    uint32_t kread_len  
);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function state(key: ByteArray | HexString): ErrorCode | ByteArray
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
#define SBUF(str) (uint32_t)(str), sizeof(str)
if (state(SBUF(vault), SBUF(vault_key)) != 16)
    rollback(SBUF("Error: could not read state!"), 1);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
const value = state(SBUF(vault), SBUF(vault_key))
if (typeof value === 'number' || value.length != 16)
    rollback("Error: could not read state!", 1);
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}
| Name       | Type      | Description                                                       |
| ---------- | --------- | ----------------------------------------------------------------- |
| write\_ptr | uint32\_t | A pointer to the buffer to write the data in the Hook State into. |
| write\_len | uint32\_t | The length of the write buffer.                                   |
| kread\_ptr | uint32\_t | Pointer to a buffer containing the Hook State key.                |
| kread\_len | uint32\_t | The length of the Hook State key. (Should be 32.)                 |

> ### 📘Hint
>
> Ensure you check the return value. A state lookup can fail of a range of reasons and the buffer will then contain whatever it did before the call (typically all zeros).
{% endtab %}

{% tab title="Javascript" %}
| Name | Type                   | Description                                           |
| ---- | ---------------------- | ----------------------------------------------------- |
| key  | ByteArray or HexString | The key of the Hook State to retrieve the value from. |
{% endtab %}
{% endtabs %}



### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The number of bytes written to the write buffer.<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.<br><br><code>DOESNT_EXIST</code><br>- the specified Hook State key doesn't have an associated value on the ledger at the time of the call.<br><br><code>TOO_BIG</code><br>- the key specified by <code>read_ptr</code> and <code>read_len</code> was larger than 32 bytes.<br><br><code>TOO_SMALL</code><br>- the output buffer was too small to store the Hook State data.</p> |
{% endtab %}

{% tab title="Javascript" %}
| Type                   | Description                                                |
| ---------------------- | ---------------------------------------------------------- |
| ByteArray or ErrorCode | Returns an error code or the Hook State value for the key. |
{% endtab %}
{% endtabs %}

