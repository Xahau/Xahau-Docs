---
description: Serialize and output a field from the originating transaction
---

# otxn\_field

### Behaviour

{% tabs %}
{% tab title="C" %}
* Find the specified `sf` field in the originating transaction
* Write the serialized version of the field to the output buffer
{% endtab %}

{% tab title="Javascript" %}
* Retrieve the value of a specific field in the originating transaction.
* Returns the value of the specified field as an array of numbers, or an ErrorCode if the lookup fails.
{% endtab %}
{% endtabs %}

### Definition

{% tabs %}
{% tab title="C" %}
```c
int64_t otxn_field (
    uint32_t write_ptr,
    uint32_t write_len,
    uint32_t field_id
);
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
function otxn_field(field_id: number): ErrorCode | ByteArray
```
{% endtab %}
{% endtabs %}



### Example

{% tabs %}
{% tab title="C" %}
```c
int64_t account_field_len = 
    otxn_field(account_field, 20, sfAccount);
```


{% endtab %}

{% tab title="Javascript" %}
```javascript
const account_field = otxn_field(sfAccount)
```
{% endtab %}
{% endtabs %}



### Parameters

{% tabs %}
{% tab title="C" %}
| Name       | Type      | Description                                                                                                                                                                                                                                                                                                                                                                                                |
| ---------- | --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| write\_ptr | uint32\_t | Pointer to a buffer of a suitable size to store the output.                                                                                                                                                                                                                                                                                                                                                |
| write\_len | uint32\_t | Length of the output buffer.                                                                                                                                                                                                                                                                                                                                                                               |
| field\_id  | uint32\_t | <p>The <code>sf</code> code of the field you are searching for.<br><br>To compute this manually take the serialized <code>type</code> and shift it into the 16 highest bits of uint32_t, then take the <code>field</code> and place it in the 16 lowest bits.<br><br>For example:<br><code>sfEmitNonce</code> has <code>type</code> 5 and <code>field</code> 11 thus its value is <code>0x050BU</code></p> |

> ### ❗️Important
>
> The field code is _not_ written to the output buffer, only the _payload_ of the field is.
>
> At time of writing for Hooks Public Testnet, `STI_ACCOUNT` fields like `sfAccount` are returned _without_ the leading variable length byte.
{% endtab %}

{% tab title="Javascript" %}
| Name      | Type   | Description                                                                                         |
| --------- | ------ | --------------------------------------------------------------------------------------------------- |
| field\_id | number | <p></p><p>Returns the value of the specified field as an array of numbers, if the lookup fails.</p> |
{% endtab %}
{% endtabs %}

### Return Code

{% tabs %}
{% tab title="C" %}
| Type     | Description                                                                                                                                                                                                                                                                                                                                                                                                                            |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| int64\_t | <p>The number of bytes written<br><br>If negative, an error:<br><code>OUT_OF_BOUNDS</code><br>- pointers/lengths specified outside of hook memory.<br><br><code>TOO_SMALL</code><br>- output buffer was not large enough to hold the serialized field<br><br><code>INVALID_FIELD</code><br>- the <code>sf</code> field_id was invalid<br><br><code>DOESNT_EXIST</code><br>- the field was not found in the originating transaction</p> |
{% endtab %}

{% tab title="Javascript" %}
| Type                   | Description                                                                                                         |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------- |
| ByteArray or ErrorCode | <p></p><p>Returns the value of the specified field as an array of numbers, or an ErrorCode if the lookup fails.</p> |
{% endtab %}
{% endtabs %}

